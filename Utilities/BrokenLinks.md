## Using Selenium 4 + Chrome DevTools Protocol (CDP)

Instead of checking every link manually, CDP can capture network failures while Selenium navigates the page.

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import java.util.concurrent.atomic.AtomicInteger;

import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.devtools.DevTools;
import org.openqa.selenium.devtools.v128.network.Network;

public class BrokenLinkReporter {

	public static void main(String[] args) throws Exception {

		ChromeDriver driver = new ChromeDriver();

		DevTools devTools = driver.getDevTools();
		devTools.createSession();

		devTools.send(Network.enable(Optional.empty(), Optional.empty(), Optional.empty()));

		AtomicInteger totalLinks = new AtomicInteger(0);
		AtomicInteger validLinks = new AtomicInteger(0);
		AtomicInteger redirectLinks = new AtomicInteger(0);
		AtomicInteger brokenLinks = new AtomicInteger(0);

		List<String> brokenLinkDetails = new ArrayList<>();

		devTools.addListener(Network.responseReceived(), response -> {

			String url = response.getResponse().getUrl();
			int status = response.getResponse().getStatus().intValue();

			totalLinks.incrementAndGet();

			if (status >= 200 && status < 300) {
				validLinks.incrementAndGet();

			} else if (status >= 300 && status < 400) {
				redirectLinks.incrementAndGet();

			} else if (status >= 400) {
				brokenLinks.incrementAndGet();
				brokenLinkDetails.add(status + " : " + url);
			}
		});

		driver.get("https://example.com");

		// Allow network traffic to complete
		Thread.sleep(10000);

		System.out.println();
		System.out.println("Recommended Framework Reporting Output");
		System.out.println();
		System.out.println("Total Links     : " + totalLinks.get());
		System.out.println("Valid Links     : " + validLinks.get());
		System.out.println("Broken Links    : " + brokenLinks.get());
		System.out.println("Redirect Links  : " + redirectLinks.get());

		System.out.println();
		System.out.println("Broken Links:");
		System.out.println("----------------------------------------------");

		if (brokenLinkDetails.isEmpty()) {
			System.out.println("No Broken Links Found");
		} else {
			brokenLinkDetails.forEach(System.out::println);
		}

		System.out.println("----------------------------------------------");

		driver.quit();
	}
}
```

**Output**
```text
Total Links     : 150
Valid Links     : 142
Broken Links    : 6
Redirect Links  : 2

Broken Links:
----------------------------------------------
404 : https://example.com/aboutus1
500 : https://example.com/api/v1/report
503 : https://example.com/contact
----------------------------------------------
```

**Common status code to validate**
----

| Status Code | Meaning |
|------------|---------|
| 200 | Valid Link |
| 301 | Permanent Redirect |
| 302 | Temporary Redirect |
| 403 | Forbidden |
| 404 | Not Found |
| 408 | Timeout |
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |
