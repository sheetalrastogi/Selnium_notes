### WireMock 

WireMock allows you to mock external APIs so that RestAssured tests can run without depending on real downstream services.


## Scenario

Suppose your application calls:

```text
GET https://customer-service/api/customers/100
```

Instead of calling the real service, WireMock will return a mocked response.

## Maven Dependencies
```xml
<dependency>
    <groupId>org.wiremock</groupId>
    <artifactId>wiremock-standalone</artifactId>
    <version>3.13.1</version>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>rest-assured</artifactId>
    <version>5.5.6</version>
    <scope>test</scope>
</dependency>
```

## Example 1: Mock GET API

** Step 1:  Start WireMock Server**

```java
import com.github.tomakehurst.wiremock.WireMockServer;

public class WireMockSetup {

	static WireMockServer wireMockServer = new WireMockServer(8089);

	public static void startServer() {
		wireMockServer.start();
	}

	public static void stopServer() {
		wireMockServer.stop();
	}
}
```

** Step 2: Create Stub**

```java
import static com.github.tomakehurst.wiremock.client.WireMock.*;

wireMockServer.stubFor(get(urlEqualTo("/api/customers/100")).willReturn(aResponse().withStatus(200).withHeader("Content-Type","application/json").withBody("""
                                      {
                                         "id":100,
                                         "name":"Sheetal",
                                         "city":"Noida"
                                      }
                                      """)));
```


** Step 3: Validate Using RestAssured**

```java
import io.restassured.RestAssured;
import org.junit.jupiter.api.Test;

import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

class CustomerApiTest {

	@Test
	void verifyCustomer() {

		given().when().get("http://localhost:8089/api/customers/100").then().statusCode(200).body("id", equalTo(100))
				.body("name", equalTo("Sheetal")).body("city", equalTo("Noida"));
	}
}

```

### Key Areas to Automate Test with WireMock

## Successful responses (200 OK)
- Verify your application processes valid API responses correctly.

## Error responses
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 500 Internal Server Error
- 503 Service Unavailable

## Timeouts and Delays
- Test application behavior when external APIs are slow or unresponsive.

## Retry Logic
- Verify retries happen as expected when an API temporarily fails.

## Request Validation
- Request body/payload
- HTTP headers
- Query parameters
- Path parameters

## Authentication & Authorization
- Invalid token
- Expired token
- Missing token

## Rate Limiting
- 429 Too Many Requests
- Backoff and retry behavior

## Contract Validation
- JSON structure
- Field mappings
- Missing or null fields

## Edge Cases
- Empty responses
- Null values
- Unexpected payloads

## Service Virtualization Mock dependencies such as:
- Payment Gateway
- Customer Service
- Inventory Service
- Shipping Service
- Fraud Detection Service
