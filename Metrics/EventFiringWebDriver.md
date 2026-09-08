## EventFiring WebDriver implementation with Selenium 4

In Selenium 4, the older EventFiringWebDriver is deprecated. The recommended approach is to use WebDriverListener together with EventFiringDecorator.

**Such WebDriver Listener is useful for**:

- Logging
- Screenshot Capture
- Retry Tracking
- Performance Timing
- Browser Audit Trails
- ExtentReports Integration
- Allure Integration
- Prometheus Metrics
- Grafana Dashboard Feeds
- Test Execution Analytics
- Self-Healing Locator Monitoring



## Step 1. Create a Custom WebDriver Listener

```java
package listeners;

import org.openqa.selenium.*;

public class CustomWebDriverListener implements WebDriverListener {

	@Override
	public void beforeGet(WebDriver driver, String url) {
		System.out.println("[BEFORE] Navigating to: " + url);
	}

	@Override
	public void afterGet(WebDriver driver, String url) {
		System.out.println("[AFTER] Successfully navigated to: " + url);
	}

	@Override
	public void beforeClick(WebElement element) {
		System.out.println("[BEFORE CLICK] " + element);
	}

	@Override
	public void afterClick(WebElement element) {
		System.out.println("[AFTER CLICK] " + element);
	}

	@Override
	public void beforeSendKeys(WebElement element, CharSequence... keysToSend) {
		System.out.println("[BEFORE SENDKEYS] " + String.join("", keysToSend));
	}

	@Override
	public void afterSendKeys(WebElement element, CharSequence... keysToSend) {
		System.out.println("[AFTER SENDKEYS] " + String.join("", keysToSend));
	}

	@Override
	public void onError(Object target, Method method, Object[] args, InvocationTargetException e) {

		System.out.println("[ERROR] Method Failed : " + method.getName());

		Throwable cause = e.getTargetException();
		System.out.println("[CAUSE] " + cause.getMessage());
	}
}
```


## Step 2. Decorate Driver with EventFiringDecorator

```java
import listeners.CustomWebDriverListener;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.events.EventFiringDecorator;

public class DriverFactory {

	public static WebDriver createDriver() {

		WebDriver originalDriver = new ChromeDriver();

		CustomWebDriverListener listener = new CustomWebDriverListener();

		WebDriver decoratedDriver = new EventFiringDecorator(listener).decorate(originalDriver);

		return decoratedDriver;
	}
}
```


## Step 3. Use Decorated Driver

```java
public class LoginTest {

    public static void main(String[] args) {

        WebDriver driver = DriverFactory.createDriver();

        driver.get("https://www.google.com");

        driver.quit();
    }
}
```

Console Output
[BEFORE] Navigating to: https://www.google.com
[AFTER] Successfully navigated to: https://www.google.com

## Step 4. Capture Element Operations 

```java
driver.findElement(By.name("q")).sendKeys("Selenium 4");

driver.findElement(By.name("q")).submit();
```

Console Output
[BEFORE SENDKEYS] Selenium 4
[AFTER SENDKEYS] Selenium 4

[BEFORE CLICK] [[ChromeDriver]]
[AFTER CLICK] [[ChromeDriver]]

## Step 5. Screenshot on Failure Listener


```java
package listeners;

import java.io.File;
import java.lang.reflect.Method;
import java.lang.reflect.InvocationTargetException;
import java.nio.file.Files;
import java.nio.file.StandardCopyOption;

import org.openqa.selenium.*;

public class ScreenshotListener implements WebDriverListener {

	@Override
	public void onError(Object target, Method method, Object[] args, InvocationTargetException e) {
		try {
			if (target instanceof WebDriver driver) {
				File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
				File dest = new File("screenshots/error_" + System.currentTimeMillis() + ".png");
				Files.copy(src.toPath(), dest.toPath(), StandardCopyOption.REPLACE_EXISTING);
				System.out.println("Screenshot Captured: " + dest.getAbsolutePath());
			}
		} catch (Exception ex) {
			ex.printStackTrace();
		}
	}
}
```
## Step 6. Enterprise Framework Logging Listener

```java
public class LoggingListener implements WebDriverListener {

	@Override
	public void beforeFindElement(WebDriver driver, By locator) {

		System.out.println("[LOCATE] Searching : " + locator);
	}

	@Override
	public void afterFindElement(WebDriver driver, By locator, WebElement result) {

		System.out.println("[FOUND] " + locator);
	}

	@Override
	public void beforeQuit(WebDriver driver) {
		System.out.println("[BROWSER] Closing Browser");
	}

	@Override
	public void afterQuit(WebDriver driver) {
		System.out.println("[BROWSER] Driver Closed");
	}
}
```

## Example Metric Collection
@Override
public void beforeClick(WebElement element) {
    MetricsRegistry.increment("selenium.click.count");
}

@Override
public void afterGet(WebDriver driver, String url) {
    MetricsRegistry.increment("selenium.page.load.count");
}


Using this pattern, it can easily be integrates with TestNG listeners, Extent Reports, Allure, Prometheus/Grafana, in an enterprise automation frameworks.
