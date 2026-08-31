If you're doing **network validation**, **API monitoring**, **security testing**, or **performance benchmarking** as part of an automation framework, both BrowserMob Proxy (BMP) and Chrome DevTools Protocol (CDP) can capture network traffic. However, CDP is generally preferred in Selenium 4 because it is built into Chrome and doesn't require a separate proxy server.

## 1. BrowserMob Proxy with Selenium 4 Java

**Maven Dependency**
```xml
<dependency>
    <groupId>net.lightbody.bmp</groupId>
    <artifactId>browsermob-core</artifactId>
    <version>2.1.5</version>
</dependency>

<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.24.0</version>
</dependency>
```

**Capture Network Traffic (HAR File)**

```java
import java.io.File;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.Proxy;
import org.openqa.selenium.chrome.ChromeOptions;

import net.lightbody.bmp.BrowserMobProxy;
import net.lightbody.bmp.BrowserMobProxyServer;
import net.lightbody.bmp.client.ClientUtil;
import net.lightbody.bmp.core.har.Har;

public class BrowserMobProxyExample {

	public static void main(String[] args) throws Exception {

        BrowserMobProxy proxy = new BrowserMobProxyServer();
        proxy.start(0);

        Proxy seleniumProxy = ClientUtil.createSeleniumProxy(proxy);

        ChromeOptions options = new ChromeOptions();
        options.setProxy(seleniumProxy);

        WebDriver driver = new ChromeDriver(options);

        proxy.newHar("Google");

        driver.get("https://www.google.com");

        Thread.sleep(5000);

        Har har = proxy.getHar();

        File harFile = new File("networkTraffic.har");
        har.writeTo(harFile);

        System.out.println("HAR File saved: " + harFile.getAbsolutePath());

        driver.quit();
        proxy.stop();
    }
}
```

**Capture API Calls**

```java
proxy.enableHarCaptureTypes(
        CaptureType.REQUEST_CONTENT,
        CaptureType.RESPONSE_CONTENT);
```

**After execution:**

```java
		Har har = proxy.getHar();

		har.getLog().getEntries().forEach(entry -> {

			System.out.println("URL: " + entry.getRequest().getUrl());

			System.out.println("Method: " + entry.getRequest().getMethod());

			System.out.println("Status: " + entry.getResponse().getStatus());

			System.out.println("--------------------");
		});
```

# Security Validation Example

**Detect HTTP traffic:**

```java
		har.getLog().getEntries().forEach(entry -> {

			String url = entry.getRequest().getUrl();

			if (url.startsWith("http://")) {
				System.out.println("WARNING: Unsecured traffic detected -> " + url);
			}

		});
```

**Detect Sensitive Data Exposure**

```java
		har.getLog().getEntries().forEach(entry -> {

			String content = entry.getResponse().getContent().getText();

			if (content != null && content.contains("password")) {

				System.out.println("Potential sensitive data found");
			}

		});
```

## 2. Selenium 4 + Chrome DevTools Protocol (Recommended)
No external proxy required.

**Capture All Network Requests**

```java
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.devtools.DevTools;

import org.openqa.selenium.devtools.v128.network.Network;
import org.openqa.selenium.devtools.v128.network.model.Request;

import java.util.Optional;

public class CDPNetworkCapture {

	public static void main(String[] args) {

		ChromeDriver driver = new ChromeDriver();

		DevTools devTools = driver.getDevTools();

		devTools.createSession();

		devTools.send(Network.enable(Optional.empty(), Optional.empty(), Optional.empty()));

		devTools.addListener(Network.requestWillBeSent(), request -> {

			Request req = request.getRequest();

			System.out.println(req.getMethod() + " " + req.getUrl());
		});

		driver.get("https://www.google.com");

		driver.quit();
	}
}
```

**Capture Response Status Codes**

```java
		devTools.addListener(Network.responseReceived(), response -> {

			System.out.println(response.getResponse().getUrl());

			System.out.println(response.getResponse().getStatus());

			System.out.println("------------------");
		});
```

**Capture API Response Bodies**

```java
		devTools.addListener(Network.responseReceived(), response -> {

			String requestId = response.getRequestId().toString();

			try {

				var body = devTools.send(Network.getResponseBody(response.getRequestId()));

				System.out.println(body.getBody());

			} catch (Exception e) {
			}
		});
```

**Detect Clear Text Credentials**
Suppose application sends:
```text
{
  "username":"admin",
  "password":"secret123"
}
```

**CDP validation:**

```java
devTools.addListener(Network.requestWillBeSent(), request -> {
	String postData = request.getRequest().getPostData().orElse("");
	if (postData.contains("password")) {
				System.out.println("Potential credential transmission detected");
				System.out.println(postData);
			}
});
```

**Measure API Performance**

```java
devTools.addListener(Network.responseReceived(), response -> {
			System.out.println("URL : " + response.getResponse().getUrl());
			System.out.println("Status : " + response.getResponse().getStatus());
			System.out.println("Protocol : " + response.getResponse().getProtocol());
});
```

**Block URLs using CDP**

Useful for resilience testing:

```java
		devTools.send(Network.setBlockedURLs(java.util.List.of("*.png", "*.jpg", "*.gif")));
		driver.get("https://example.com");
```

**Capture Failed Network Requests**

```java
devTools.addListener(Network.loadingFailed(), failure -> {
		System.out.println("Request Failed : " + failure.getErrorText());
		System.out.println("Request ID : " + failure.getRequestId());
});
```

## BrowserMob Proxy(BMP) vs Chrome Dev Protocol (CDP)

| Feature | BrowserMob Proxy | CDP (Chrome DevTools Protocol) |
|----------|----------|----------|
| Capture HTTP/HTTPS | Y     | Y     |
| HAR Generation | Y     Native | N     Manual |
| Modify Requests | Y     | Y     |
| Modify Responses | Y     | Limited |
| Additional Proxy Server | Required | Not Required |
| Chrome Support | Y     | Y     |
| Edge Support | Y     | Y     |
| Firefox Support | Y     | N     |
| Performance Overhead | Higher | Lower |
| Selenium 4 Native | N     | Y     |

QA Usage Recommendation

For a Senior Test Architect designing a modern Selenium 4 framework:  86

**Use CDP for**
- API monitoring
- Security validation
- Capture request/response
- Performance metrics
- Broken links
- Network failures
- Contract validation
- Frontend observability

**Use BrowserMob Proxy for**
- HAR generation
- Legacy browser support
- Network throttling
- Advanced request/response manipulation
- Detailed audit logging



