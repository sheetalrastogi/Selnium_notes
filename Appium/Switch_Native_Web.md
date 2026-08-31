## Switch Between Native App and WebView

Hybrid mobile applications contain both:

NATIVE_APP → Native Android/iOS screens
WEBVIEW → Embedded browser content rendered inside the app

Appium allows switching between these contexts using:

```java
driver.getContextHandles();
driver.context("WEBVIEW_xxx");
driver.context("NATIVE_APP");
```


## Example 1: Switch from Native App to WebView

```java
import io.appium.java_client.android.AndroidDriver;

import java.util.Set;

public class HybridAppExample {

	public static void main(String[] args) {

		AndroidDriver driver = DriverFactory.getDriver();

		try {
			// Native App Context
			System.out.println("Current Context: " + driver.getContext());

			// Print all available contexts
			Set<String> contexts = driver.getContextHandles();
			System.out.println("Available Contexts:");

			for (String context : contexts) {
				System.out.println(context);
			}

			// Switch to WebView
			for (String context : contexts) {
				if (context.contains("WEBVIEW")) {
					driver.context(context);
					System.out.println("Switched To: " + context);
					break;
				}
			}

			// Perform Web Operations
			System.out.println("Current URL: " + driver.getCurrentUrl());
			System.out.println("Title: " + driver.getTitle());

			// Return to Native App
			driver.context("NATIVE_APP");

			System.out.println("Switched Back To Native");

		} finally {
			driver.quit();
		}
	}
}
```


**Always print contexts before switching:**

```java
driver.getContextHandles().forEach(System.out::println);
```

output:
NATIVE_APP
WEBVIEW_com.myapp

or

NATIVE_APP
WEBVIEW_12345
CHROMIUM
