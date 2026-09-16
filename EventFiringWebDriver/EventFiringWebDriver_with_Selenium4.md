## EventFiring WebDriver

In Selenium 4, the old **EventFiringWebDriver** class from Selenium 3 has been deprecated/removed and replaced with the **EventFiringDecorator** and **WebDriverListener** APIs.

### Step 1: Create a WebDriverListener

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.events.WebDriverListener;

public class WebDriverEventListener implements WebDriverListener {
    @Override
    public void beforeGet(WebDriver driver, String url) {
        System.out.println("Navigating to: " + url);
    }

    @Override
    public void afterGet(WebDriver driver, String url) {
        System.out.println("Navigation completed: " + url);
    }

    @Override
    public void beforeClick(WebElement element) {
        System.out.println("Clicking on: " + element);
    }

    @Override
    public void afterClick(WebElement element) {
        System.out.println("Clicked on: " + element);
    }

    @Override
    public void beforeQuit(WebDriver driver) {
        System.out.println("Closing browser...");
    }
}
```

### Step 2: Register Listener using EventFiringDecorator

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.events.EventFiringDecorator;

public class DriverFactory {

    public static WebDriver createDriver() {

        WebDriver originalDriver = new ChromeDriver();

        WebDriverListener listener = new WebDriverEventListener();

        WebDriver decoratedDriver = new EventFiringDecorator(listener).decorate(originalDriver);

        return decoratedDriver;
    }
}
```

### Step 3: Use Decorated Driver

```java
public class TestClass {

    public static void main(String[] args) {

        WebDriver driver = DriverFactory.createDriver();

        driver.get("https://www.google.com");

        driver.quit();
    }
}
```

**Output**
```text
Navigating to: https://www.google.com
Navigation completed: https://www.google.com
Closing browser...
```

### Common Events You Can Intercept

```text
beforeGet()
afterGet()

beforeClick()
afterClick()

beforeFindElement()
afterFindElement()

beforeSendKeys()
afterSendKeys()

beforeQuit()
afterQuit()

beforeNavigateBack()
afterNavigateBack()

beforeNavigateForward()
afterNavigateForward()

beforeAccept()
afterAccept()

beforeDismiss()
afterDismiss()

onError()
```

### Another Example:  Capturing Screenshots on Failure

```java
public class FrameworkWebDriverListener implements WebDriverListener {

    @Override
    public void onError(
            Object target,
            java.lang.reflect.Method method,
            Object[] args,
            InvocationTargetException e) {

        System.out.println("Error occurred in : "
                + method.getName());

        WebDriver driver = DriverManager.getDriver();

        File src = ((TakesScreenshot) driver)
                .getScreenshotAs(OutputType.FILE);

        // Copy to reports/screenshots folder
    }
}
```

### Selenium 4 Registration (One-Liner)

```java
WebDriver driver =
    new EventFiringDecorator(new FrameworkWebDriverListener())
        .decorate(new ChromeDriver());
```
