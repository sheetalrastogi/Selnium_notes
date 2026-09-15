### Automatically Switch to WireMock When Real Endpoint Is Unavailable

A common enterprise pattern is:

```text
1. Check Real API Health
         |
         +--> API Healthy
         |         |
         |         v
         |   Run RestAssured Against Real API
         |
         +--> API Down / Returning 5xx / Unstable
                   |
                   v
            Start WireMock
                   |
                   v
            Use Mock Response
                   |
                   v
          Continue RestAssured Tests
```

This allows your CI/CD pipeline to continue execution even when downstream systems are unavailable.

### Step 1: Create Health Checker

```java
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class EndpointHealthChecker {

	public static boolean isEndpointHealthy(String url) {

		try {
			Response response = RestAssured.given().relaxedHTTPSValidation().when().get(url);

			int statusCode = response.getStatusCode();

			return statusCode >= 200 && statusCode < 300;

		} catch (Exception e) {

			System.out.println("Endpoint not reachable: " + e.getMessage());

			return false;
		}
	}
}
```

### Step 2: WireMock Manager

```java
import com.github.tomakehurst.wiremock.WireMockServer;

import static com.github.tomakehurst.wiremock.client.WireMock.*;

public class WireMockManager {

	private static final WireMockServer server = new WireMockServer(8089);

	public static void startMockServer() {

		if (!server.isRunning()) {

			server.start();

			server.stubFor(get(urlEqualTo("/api/customers/100"))
					.willReturn(aResponse().withStatus(200).withHeader("Content-Type", "application/json").withBody("""
							{
							  "id": 100,
							  "name": "Mock Customer",
							  "city": "Noida"
							}
							""")));

			System.out.println("WireMock Started");
		}
	}

	public static void stopMockServer() {

		if (server.isRunning()) {
			server.stop();
			System.out.println("WireMock Stopped");
		}
	}
}
```

### Step 3: Step 3: Smart Base URL Selection

```java
public class EnvironmentManager {

	private static final String REAL_API = "https://customer-service/api/customers/100";

	private static final String MOCK_API = "http://localhost:8089/api/customers/100";

	public static String getApiEndpoint() {

		boolean healthy = EndpointHealthChecker.isEndpointHealthy(REAL_API);

		if (healthy) {

			System.out.println("Using Real Endpoint");

			return REAL_API;

		} else {

			System.out.println("Using WireMock");

			WireMockManager.startMockServer();

			return MOCK_API;
		}
	}
}
```

### Step 4: RestAssured Test

Now RestAssured automatically decides which endpoint to use.

```java
import org.testng.annotations.AfterClass;
import org.testng.annotations.Test;

import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

public class CustomerApiTest {

    @Test
    public void verifyCustomer() {

        // Auto-switch between Real API and WireMock
        String endpoint = EnvironmentManager.getApiEndpoint();

        System.out.println("Executing API: " + endpoint);

        given()
            .log().all()
        .when()
            .get(endpoint)
        .then()
            .log().all()
            .statusCode(200)
            .body("id", equalTo(100))
            .body("name", notNullValue());
    }

    @AfterClass
    public void tearDown() {
        WireMockManager.stopMockServer();
    }
}
```

