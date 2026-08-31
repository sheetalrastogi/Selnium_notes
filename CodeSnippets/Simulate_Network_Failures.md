## Emulate Network failures with Chrome DevTools Protocol (CDP) 

Some of the common network Network failure conditions that needs to be automated during Automation testing with Selenium 4 Java:

- No internet connection available
- Communication with server failed
- Cannot establish a connection to the server
- Resource not found
- Connection timed out
- Unable to process response from server


## Step 1: Pre-requisite - Selenium 4 + CDP Setup

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.devtools.DevTools;

WebDriver driver = new ChromeDriver();

DevTools devTools = ((ChromeDriver) driver).getDevTools();
devTools.createSession();

```

## Example 1: Simulate No Internet Connection Available

Equivalent to turning off WiFi/network.

```java
devTools.send(Network.enable(java.util.Optional.empty(),java.util.Optional.empty(),java.util.Optional.empty()));

devTools.send(Network.emulateNetworkConditions(true, // offline
0,0,0,java.util.Optional.empty()));

driver.get("https://www.google.com");
```

## Example 2: Communication With Server Failed

```java
import org.openqa.selenium.devtools.v139.fetch.Fetch;
import org.openqa.selenium.devtools.v139.fetch.model.RequestPattern;
import org.openqa.selenium.devtools.v139.network.model.ErrorReason;

devTools.send(Fetch.enable(java.util.List.of(new RequestPattern(java.util.Optional.of("*"),java.util.Optional.empty(),java.util.Optional.empty())),java.util.Optional.of(false)));

devTools.addListener(Fetch.requestPaused(),request->{

devTools.send(Fetch.failRequest(request.getRequestId(),ErrorReason.FAILED));});

driver.get("https://your-app-url");
```

## Example 3: Cannot Establish Connection To Server

Simulate connection refused.

```java
devTools.send(Fetch.enable(java.util.List.of(new RequestPattern(java.util.Optional.of("*"), java.util.Optional.empty(), java.util.Optional.empty())), java.util.Optional.empty()));

devTools.addListener(Fetch.requestPaused(), request -> devTools.send(Fetch.failRequest(request.getRequestId(), ErrorReason.CONNECTION_REFUSED)));

```

## Example 4: Resource Not Found (404)

Intercept response and return 404.

```java
devTools.send(Fetch.enable(java.util.List.of(new RequestPattern(java.util.Optional.of("*"), java.util.Optional.empty(), java.util.Optional.empty())),
				java.util.Optional.empty()));

devTools.addListener(Fetch.requestPaused(), request -> {
			devTools.send(Fetch.fulfillRequest(request.getRequestId(), 404, java.util.List.of(),
			java.util.Optional.empty(), java.util.Optional.empty(), java.util.Optional.empty()));
		});

driver.get("https://your-app-url");

```

## Example 5: Connection Timed Out

Simulate extremely slow network.

```java
devTools.send(Network.enable(java.util.Optional.empty(), java.util.Optional.empty(), java.util.Optional.empty()));

devTools.send(Network.emulateNetworkConditions(false, 60000, // 60 sec latency
				1, 1, java.util.Optional.empty()));

driver.get("https://your-app-url");

```

## Example 6: Unable To Process Response From Server

Simulate malformed response.

```java
devTools.send(Fetch.enable(java.util.List.of(new RequestPattern(java.util.Optional.of("*"), java.util.Optional.empty(), java.util.Optional.empty())),
				java.util.Optional.empty()));

devTools.addListener(Fetch.requestPaused(), req -> {
		devTools.send(Fetch.fulfillRequest(req.getRequestId(), 200, java.util.List.of(),
			java.util.Optional.of("Invalid Response Data"), java.util.Optional.empty(), java.util.Optional.empty()));
});

```
