## POM for Mobile automation

This pattern keeps locators inside the Page Class, supports both Android and iOS, and exposes only business actions such as enterUsername() and getUsernameText() to test classes.


# Step 1. Generic class to detect driver type

```java
public class PlatformLocator {

	private final By android;
	private final By ios;

	public PlatformLocator(By android, By ios) {
		this.android = android;
		this.ios = ios;
	}

	public By resolve(AppiumDriver driver) {
		if (driver instanceof AndroidDriver) {
			return android;
		}

		if (driver instanceof IOSDriver) {
			return ios;
		}

		throw new UnsupportedOperationException("Unsupported platform");
	}
}
```

# Step 2. Page Class

```java
import org.openqa.selenium.WebElement;
import io.appium.java_client.AppiumDriver;
import io.appium.java_client.AppiumBy;

public class LoginPage {

	private final AppiumDriver driver;

	public LoginPage(AppiumDriver driver) {
		this.driver = driver;
	}

	private final PlatformLocator usernameTextBox = new PlatformLocator(
			// Android
			AppiumBy.androidUIAutomator("new UiSelector().resourceId(\"com.myapp:id/txtUsername\")"),

			// iOS
			AppiumBy.iOSNsPredicateString("type == 'XCUIElementTypeTextField' AND name == 'txtUsername'")
	);


	public void enterUsername(String username) {
		driver.findElement(usernameTextBox.resolve(driver)).sendKeys(username);
	}

	public String getUsernameText() {
		return driver.findElement(usernameTextBox.resolve(driver)).getText();
	}
}
```


**Usage**

```java
LoginPage loginPage = new LoginPage(driver);
loginPage.enterUsername("admin");

String value = loginPage.getUsernameText();
System.out.println(value);
```




