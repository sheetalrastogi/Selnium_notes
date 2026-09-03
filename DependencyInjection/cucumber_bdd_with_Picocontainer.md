Examples:
https://github.com/julianogpc/cucumber-picocontainer




For a modern **Selenium 4 + Java + Cucumber 7 + PicoContainer** automation framework, recommended features:

- PicoContainer-based dependency injection
- Selenium 4 WebDriverManager support
- Page Object Model (POM)
- Thread-safe DriverManager
- Scenario Context sharing
- Hooks lifecycle management
- Extent/Allure reporting
- Config-driven execution
- Parallel execution support
- API and DB layer injection capability




**Recommended Framework Architecture**

```text
src
├── test
│   ├── java
│   │
│   ├── runners
│   │     └── TestRunner.java
│   │
│   ├── hooks
│   │     └── Hooks.java
│   │
│   ├── di
│   │     ├── TestContext.java
│   │     ├── ScenarioContext.java
│   │     └── DependencyContainer.java
│   │
│   ├── driver
│   │     └── DriverManager.java
│   │
│   ├── pages
│   │     ├── LoginPage.java
│   │     └── DashboardPage.java
│   │
│   ├── steps
│   │     ├── LoginSteps.java
│   │     └── DashboardSteps.java
│   │
│   ├── utils
│   │     ├── ConfigReader.java
│   │     ├── WaitHelper.java
│   │     └── ScreenshotUtil.java
│   │
│   └── resources
│         ├── features
│         │     └── login.feature
│         │
│         └── config.properties

```


**Maven Dependencies**

```xml
<dependencies>

    <!-- Selenium -->
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.35.0</version>
    </dependency>

    <!-- Cucumber -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-java</artifactId>
        <version>7.23.0</version>
    </dependency>

    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-testng</artifactId>
        <version>7.23.0</version>
    </dependency>

    <!-- PicoContainer -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-picocontainer</artifactId>
        <version>7.23.0</version>
    </dependency>

    <!-- WebDriverManager -->
    <dependency>
        <groupId>io.github.bonigarcia</groupId>
        <artifactId>webdrivermanager</artifactId>
        <version>6.3.2</version>
    </dependency>

</dependencies>
```

## DriverManager

```java
package driver;

import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class DriverManager {

    private WebDriver driver;

    public DriverManager() {

        WebDriverManager.chromedriver().setup();

        driver = new ChromeDriver();
        driver.manage().window().maximize();
    }

    public WebDriver getDriver() {
        return driver;
    }

    public void quit() {
        if(driver != null) {
            driver.quit();
        }
    }
}
```

## Scenario Context

Shared state between multiple step files.

```java
package di;

import java.util.HashMap;
import java.util.Map;

public class ScenarioContext {

    private final Map<String,Object> data = new HashMap<>();

    public void set(String key, Object value) {
        data.put(key, value);
    }

    public Object get(String key) {
        return data.get(key);
    }
}
```

## Test Context

Central dependency object.

```java
package di;

import driver.DriverManager;
import pages.LoginPage;

public class TestContext {

    private final DriverManager driverManager;
    private final ScenarioContext scenarioContext;

    private LoginPage loginPage;

    public TestContext() {
        driverManager = new DriverManager();
        scenarioContext = new ScenarioContext();
    }

    public DriverManager getDriverManager() {
        return driverManager;
    }

    public ScenarioContext getScenarioContext() {
        return scenarioContext;
    }

    public LoginPage getLoginPage() {

        if(loginPage == null) {
            loginPage = new LoginPage(driverManager.getDriver());
        }

        return loginPage;
    }
}
```

## Login Page

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class LoginPage {

    private final WebDriver driver;

    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    private final By username = By.id("username");
    private final By password = By.id("password");
    private final By loginButton = By.id("login");

    public void open() {
        driver.get("https://example.com/login");
    }

    public void login(String user,String pass) {
        driver.findElement(username).sendKeys(user);
        driver.findElement(password).sendKeys(pass);
        driver.findElement(loginButton).click();
    }
}
```


## Hooks

PicoContainer automatically injects TestContext.

```java
package hooks;

import di.TestContext;
import io.cucumber.java.After;
import io.cucumber.java.Before;

public class Hooks {

    private final TestContext context;

    public Hooks(TestContext context) {
        this.context = context;
    }

    @Before
    public void beforeScenario() {

        System.out.println(
            "Starting scenario...");
    }

    @After
    public void afterScenario() {

        context.getDriverManager().quit();
    }
}
```

## Login Step Definition

Notice there is no object creation.

```java
package steps;

import di.TestContext;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.When;

public class LoginSteps {

    private final TestContext context;

    public LoginSteps(TestContext context) {
        this.context = context;
    }

    @Given("user opens login page")
    public void openLoginPage() {

        context.getLoginPage().open();
    }

    @When("user login with valid credentials")
    public void login() {

        context.getLoginPage()
                .login("admin","admin123");

        context.getScenarioContext()
                .set("loggedIn", true);
    }
}
```

## Dashboard Step Definition

Demonstrates data sharing via PicoContainer.

```java
package steps;

import di.TestContext;
import io.cucumber.java.en.Then;

import static org.testng.Assert.assertTrue;

public class DashboardSteps {

    private final TestContext context;

    public DashboardSteps(TestContext context) {
        this.context = context;
    }

    @Then("user should land on dashboard")
    public void verifyDashboard() {

        Boolean loggedIn = (Boolean) context.getScenarioContext().get("loggedIn");
        assertTrue(loggedIn);
    }
}
```

## Feature File

```text
Feature: Login

  Scenario: Successful Login

    Given user opens login page
    When user login with valid credentials
    Then user should land on dashboard
```

## Cucumber Runner

```java
package runners;

import io.cucumber.testng.AbstractTestNGCucumberTests;
import io.cucumber.testng.CucumberOptions;

@CucumberOptions(
        features = "src/test/resources/features",
        glue = {
                "steps",
                "hooks"
        },
        plugin = {
                "pretty",
                "html:target/cucumber-report.html"
        }
)
public class TestRunner
        extends AbstractTestNGCucumberTests {
}
```

## Why PicoContainer Is Better Than Static Driver Patterns

```text
Traditional Framework

Step1 --> BaseClass.getDriver()
Step2 --> BaseClass.getDriver()
Step3 --> BaseClass.getDriver()

Problems
---------
Static state
Hard to parallelize
Poor test isolation


PicoContainer Framework

Scenario
   │
   ├── TestContext
   │      ├── DriverManager
   │      ├── ScenarioContext
   │      └── PageObjects
   │
   ├── LoginSteps
   └── DashboardSteps
```

**Benefits**:

- Constructor-based injection
- No Singleton anti-pattern
- No static WebDriver
- Scenario-scoped state
- Easily parallelizable
- Clean separation of concerns
- Supports Selenium, API, DB, Kafka, FTP, Appium dependencies through the same context


## Optional: DependencyContainer (Enterprise Style)

If you have many dependencies eg:

- WebDriver
- API Client
- Database Helper
- Kafka Client
- FTP Helper
- Config Manager
- Soft Assertions
- Extent Report Manager

then a dedicated container becomes useful example:

```java
package di;

import driver.DriverManager;
import utils.ConfigReader;
import utils.WaitHelper;

public class DependencyContainer {

    private final DriverManager driverManager;
    private final ConfigReader configReader;
    private final WaitHelper waitHelper;
    private final ScenarioContext scenarioContext;

    public DependencyContainer() {

        driverManager = new DriverManager();
        configReader = new ConfigReader();
        waitHelper = new WaitHelper(driverManager.getDriver());

        scenarioContext = new ScenarioContext();
    }

    public DriverManager getDriverManager() {
        return driverManager;
    }

    public ConfigReader getConfigReader() {
        return configReader;
    }

    public WaitHelper getWaitHelper() {
        return waitHelper;
    }

    public ScenarioContext getScenarioContext() {
        return scenarioContext;
    }
}
```


**LoginPage using DependencyContainer**

```java
public class LoginPage {

    private final DependencyContainer container;

    public LoginPage(DependencyContainer container) {
        this.container = container;
    }

    public void open() {
        container.getDriverManager()
                 .getDriver()
                 .get(container.getConfigReader().getBaseUrl());
    }
}
```

**Step Definition**

```java
public class LoginSteps {

    private final DependencyContainer container;
    private final LoginPage loginPage;

    public LoginSteps(DependencyContainer container, LoginPage loginPage) {
        this.container = container;
        this.loginPage = loginPage;
    }

    @Given("user launches application")
    public void launchApplication() {
        loginPage.open();
    }
}
```


