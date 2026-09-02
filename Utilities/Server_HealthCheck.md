

```java
import io.restassured.RestAssured;
import java.time.Duration;

public class HealthCheckUtil {

	public static void waitUntilHealthy(String endpoint, Duration timeout, Duration pollingInterval) {
		long endTime = System.currentTimeMillis() + timeout.toMillis();
		while (System.currentTimeMillis() < endTime) {
			try {
				int statusCode = RestAssured.given().relaxedHTTPSValidation().get(endpoint).getStatusCode();
				if (statusCode == 200) {
					return;
				}
			} catch (Exception ignored) {
			}

			try {
				Thread.sleep(pollingInterval.toMillis());
			} catch (InterruptedException e) {
				Thread.currentThread().interrupt();
			}
		}
		throw new RuntimeException("Application failed health check within timeout");
	}
}
```
**Usage**

```java
@BeforeSuite
public void verifyApplicationStarted() {
    HealthCheckUtil.waitUntilHealthy(
            "https://api.mycompany.com/actuator/health",
            Duration.ofMinutes(2),
            Duration.ofSeconds(10));
}
```

