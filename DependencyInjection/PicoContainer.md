## Dependency Injection (DI) using PicoContainer


The example demonstrates how a Selenium-style framework can inject dependencies (WebDriver, Page Objects, Services) without creating objects manually using new.

## 1. Maven Dependency
```xml
<dependency>
    <groupId>org.picocontainer</groupId>
    <artifactId>picocontainer</artifactId>
    <version>2.15</version>
</dependency>
```


## 2. Business Service

```java
package com.example.service;

public class LoginService {

    public void login(String username, String password) {
        System.out.println("Logging in user: " + username);
    }
}
```

## 3. Page Object

Notice that LoginService is injected through the constructor.

```java
package com.example.pages;

import com.example.service.LoginService;

public class LoginPage {

	private final LoginService loginService;

	public LoginPage(LoginService loginService) {
		this.loginService = loginService;
	}

	public void loginToApplication(String username, String password) {
		loginService.login(username, password);
		System.out.println("LoginPage operation completed.");
	}
}
```

## 4. Test Class

Notice there is no object creation using new LoginPage().

```java
package com.example.tests;

import com.example.pages.LoginPage;

public class LoginTest {

	private final LoginPage loginPage;

	public LoginTest(LoginPage loginPage) {
		this.loginPage = loginPage;
	}

	public void executeTest() {
		loginPage.loginToApplication("admin", "password123");
	}
}
```


## 5. PicoContainer Configuration

```java
package com.example.runner;

import org.picocontainer.DefaultPicoContainer;

import com.example.pages.LoginPage;
import com.example.service.LoginService;
import com.example.tests.LoginTest;

public class TestRunner {

	public static void main(String[] args) {

		DefaultPicoContainer container = new DefaultPicoContainer();

		// Register components
		container.addComponent(LoginService.class);
		container.addComponent(LoginPage.class);
		container.addComponent(LoginTest.class);

		// Resolve entire dependency graph automatically
		LoginTest test = container.getComponent(LoginTest.class);

		test.executeTest();
	}
}
```


**Output**

```text
Logging in user: admin
LoginPage operation completed.
```

## Typical Selenium Framework Usage

PicoContainer is commonly used to inject:

```text
Container
│
├── ConfigManager
├── DriverManager
├── WaitHelper
├── ApiClient
├── DatabaseHelper
├── LoginPage
├── DashboardPage
└── LoginTest
```

In traditional call (to login functionality)

```java
LoginPage page = new LoginPage(
        new DriverManager(),
        new ConfigManager(),
        new WaitHelper());
```

With Pico-container calling login functionality is simply by calling picocontainer

```java
LoginPage page = container.getComponent(LoginPage.class);
```

