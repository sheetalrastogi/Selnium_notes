## Internationalization Testing (i18n Testing) 

i18n Testing is the process of validating that an application can correctly support 
- multiple languages, 
- locales, 
- regional settings, 
- character sets, 
- cultural formats, and 
- input methods without requiring code changes.

The goal is to ensure the application works correctly for users worldwide regardless of:

  - Language (English, Hindi, Japanese, Arabic, Chinese, French, etc.)
  - Character encoding (UTF-8, Unicode)
  - Locale-specific formats
  - Date (31/08/2026, 08/31/2026)
  - Time (12-hour, 24-hour)
  - Currency (₹, $, €)
  - Numbers (1,000.50 vs 1.000,50)
  - Right-to-Left (RTL) languages
  - Arabic
  - Hebrew
  - Special characters and Unicode symbols
  - IME (Input Method Editor) support

Examples of Internationalized Input
```text
English      : John Smith
French       : François Dupont
German       : Müller
Spanish      : José García
Hindi        : अमित कुमार
Chinese      : 张伟
Japanese     : 山田太郎
Korean       : 김민수
Arabic       : محمد أحمد
Russian      : Иван Иванов
Thai         : สมชาย ใจดี
```

Typical Page class consideration for Internationalization Test
- Verify WebElements accepts text as per system's locale
- Validate messages appear correctly as per system's locale:


## Approach

Below is an enterprise-grade Selenium 4 Java Page Object Model design for Internationalization (i18n) testing using Resource Bundles. This approach keeps locale-specific test data outside the test code and automatically loads values based on the system locale.


Project structure:

```text
src/test/resources
│
├── login-users.properties
├── login-users_fr.properties
├── login-users_hi.properties
├── login-users_ja.properties
│
src/test/java
│
├── pages
│   └── LoginPage.java
│
├── utilities
│   └── I18nResourceManager.java
│
└── tests
    └── LoginI18nTest.java
```

## Step 1. Create Resource Bundles

Instead of hardcoding locale strings, store them in resource bundles. eg.

```text
login-users.properties
	username=John Smith

login-users_fr.properties
	username=François Dupont

login-users_hi.properties
	username=अमित कुमार
login-users_ja.properties
	username=山田太郎
```

## Step 2. Resource Bundle Utility

This utility loads locale-specific values automatically.


```java
package utilities;

import java.util.Locale;
import java.util.ResourceBundle;

public class I18nResourceManager {

	private static final ResourceBundle BUNDLE = ResourceBundle.getBundle("login-users", Locale.getDefault());

	private I18nResourceManager() {
	}

	public static String getValue(String key) {
		return BUNDLE.getString(key);
	}

	public static Locale getCurrentLocale() {
		return Locale.getDefault();
	}
}
```

## Step 3. Step 3: Login Page Object

The Page Object itself becomes locale-aware.


```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import utilities.I18nResourceManager;

public class LoginPage {

	private final WebDriver driver;

	private final By usernameTextbox = By.id("username");
	private final By passwordTextbox = By.id("password");
	private final By loginButton = By.id("loginBtn");

	public LoginPage(WebDriver driver) {
		this.driver = driver;
	}

	public LoginPage enterUsername(String username) {
		driver.findElement(usernameTextbox).clear();
		driver.findElement(usernameTextbox).sendKeys(username);
		return this;
	}

	public LoginPage enterPassword(String password) {
		driver.findElement(passwordTextbox).clear();
		driver.findElement(passwordTextbox).sendKeys(password);
		return this;
	}

	public void clickLogin() {
		driver.findElement(loginButton).click();
	}

	public void login(String username, String password) {
		enterUsername(username);
		enterPassword(password);
		clickLogin();
	}

	// Internationalization-aware login
	public void loginUsingCurrentLocale() {
		login(I18nResourceManager.getValue("username"), I18nResourceManager.getValue("password"));
	}
}
```

## Step 4: Test Class

Simple test using locale-specific values.

```java
package tests;

import org.testng.annotations.Test;
import pages.LoginPage;
import utilities.I18nResourceManager;

public class LoginI18nTest extends BaseTest {

@Test
public void verifyLoginWithLocalizedUser() {
	LoginPage loginPage = new LoginPage(driver);
	loginPage.login(I18nResourceManager.getValue("username"), I18nResourceManager.getValue("password"));
	System.out.println("Locale : " + I18nResourceManager.getCurrentLocale());
	System.out.println("Username : " + I18nResourceManager.getValue("username"));
 }
}
```

