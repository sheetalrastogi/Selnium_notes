Waits in Selenium:

**Implicit Wait**

Applied globally to all element searches.

```java
import java.time.Duration;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

WebDriver driver = new ChromeDriver();
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
driver.get("https://example.com");
// Selenium will keep trying for up to 10 seconds
driver.findElement(By.id("username")).sendKeys("admin");
```

**Explicit Wait**

Waits for a specific condition before proceeding.

```java
import java.time.Duration;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.openqa.selenium.support.ui.ExpectedConditions;

WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(15));
WebElement loginButton = wait.until(ExpectedConditions.elementToBeClickable(By.id("loginBtn")));
loginButton.click();
```


Other Examples:

```java
wait.until(ExpectedConditions.numberOfElementsToBeMoreThan(By.cssSelector(".item"), 5));

// Wait for Title
wait.until(ExpectedConditions.titleContains("Home"));

// Wait for URL Change
wait.until(ExpectedConditions.urlContains("dashboard"));

// Wait for Frame and Switch to it
wait.until(ExpectedConditions.frameToBeAvailableAndSwitchToIt("paymentFrame"));

// Wait for Alert
Alert alert = wait.until(ExpectedConditions.alertIsPresent());
	  alert.accept();
	  
// Wait for Text to Appear
wait.until(ExpectedConditions.textToBePresentInElementLocated(By.id("status"),"Completed"));

// Wait for Invisibility of Element
wait.until(ExpectedConditions.invisibilityOfElementLocated(By.id("loadingSpinner")));

// Wait for Element to be Clickable
WebElement submitBtn = wait.until(ExpectedConditions.elementToBeClickable(By.id("submit")));
		   submitBtn.click();

// Wait for Visibility of Element
WebElement username = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
		   username.sendKeys("testuser");

// Wait for Presence of Element
WebElement element = wait.until(ExpectedConditions.presenceOfElementLocated(By.cssSelector(".product")));



```

**Fluent Wait**

Allows polling interval and exception handling customization.

```java
import java.time.Duration;
import org.openqa.selenium.support.ui.FluentWait;

Wait<WebDriver> fluentWait =
        new FluentWait<>(driver)
                .withTimeout(Duration.ofSeconds(30))
                .pollingEvery(Duration.ofSeconds(2))
                .ignoring(NoSuchElementException.class);

WebElement element = fluentWait.until(
        d -> d.findElement(By.id("searchBox")));

element.sendKeys("Selenium");
```

**Custom Lambda Wait**

```java
new WebDriverWait(driver, Duration.ofSeconds(20))
        .until(driver -> driver.findElement(
                By.id("status"))
                .getText()
                .equalsIgnoreCase("SUCCESS"));
```


**JavaScript Page load and Ready State Wait**

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(20));

wait.until(driver ->
    ((JavascriptExecutor) driver)
        .executeScript("return document.readyState")
        .equals("complete"));
```


**Page Load Timeout**

Defines the maximum time Selenium waits for a page to fully load.

```java
driver.manage().timeouts().pageLoadTimeout(Duration.ofSeconds(30));
```

**Script Timeout**

Controls how long Selenium waits for JavaScript execution initiated through JavascriptExecutor.

```java
driver.manage().timeouts()
      .scriptTimeout(Duration.ofSeconds(5));

JavascriptExecutor js = (JavascriptExecutor) driver;

js.executeAsyncScript(
    "var callback = arguments[arguments.length - 1];" +
    "window.setTimeout(function() {" +
    "   callback('Completed');" +
    "}, 3000);"
);
```

## Selenium Timeout Cheat Sheet

| Timeout Type | Purpose | Typical Value |
|--------------|----------|---------------|
| Implicit Wait | Wait for element presence | 5-10 sec |
| Explicit Wait | Wait for specific condition | 10-30 sec |
| Fluent Wait | Custom polling strategy | 10-30 sec |
| Page Load Timeout | Wait for page load completion | 30-60 sec |
| Script Timeout | Wait for Async JavaScript execution | 10-30 sec |

### Best Practices

- Prefer **Explicit Wait (`WebDriverWait`)** for element synchronization.
- Keep **Implicit Wait** low (0-5 seconds) or avoid mixing it with Explicit Waits.
- Use **Script Timeout** only when executing asynchronous JavaScript via `executeAsyncScript()`.
- Configure **Page Load Timeout** for applications with slow-loading pages.
- Use **Fluent Wait** when you need custom polling intervals and exception handling.
