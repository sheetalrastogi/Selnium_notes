## WebDriver Instantiation with Factory Design Pattern

A typical implementation involves:
- **Interface** → Defines driver operations.
- **Factory Pattern** → Creates browser-specific WebDriver objects.
- **Driver Manager** → Maintains driver instance using ThreadLocal for parallel execution.
- **Capabilities Support** → Store and retrieve browser capabilities.


### 1. Driver Interface

```java
package com.framework.driver;

import org.openqa.selenium.Capabilities;
import org.openqa.selenium.WebDriver;

public interface DriverProvider {

    WebDriver getDriver();

    Capabilities getDriverCapabilities();

    void setDriverCapabilities(Capabilities capabilities);
}
```

### 2. Browser Type Enum

```java
package com.framework.driver;

public enum BrowserType {
    CHROME,
    FIREFOX,
    EDGE
}
```


### 3. Driver Factory

```java
package com.framework.driver;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.edge.EdgeOptions;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.firefox.FirefoxOptions;

public class WebDriverFactory {

	public static WebDriver createDriver(BrowserType browser, org.openqa.selenium.Capabilities capabilities) {

		switch (browser) {

		case CHROME:
			ChromeOptions chromeOptions = new ChromeOptions();
			if (capabilities != null) {
				chromeOptions.merge(capabilities);
			}
			return new ChromeDriver(chromeOptions);

		case FIREFOX:
			FirefoxOptions firefoxOptions = new FirefoxOptions();
			if (capabilities != null) {
				firefoxOptions.merge(capabilities);
			}
			return new FirefoxDriver(firefoxOptions);

		case EDGE:
			EdgeOptions edgeOptions = new EdgeOptions();
			if (capabilities != null) {
				edgeOptions.merge(capabilities);
			}
			return new EdgeDriver(edgeOptions);

		default:
			throw new IllegalArgumentException("Unsupported Browser: " + browser);
		}
	}
}
```

### 4. Driver Manager Implementation


```java
package com.framework.driver;

import org.openqa.selenium.Capabilities;
import org.openqa.selenium.WebDriver;

public class DriverManager implements DriverProvider {

	private static final ThreadLocal<WebDriver> DRIVER = new ThreadLocal<>();

	private static final ThreadLocal<Capabilities> CAPABILITIES = new ThreadLocal<>();

	public DriverManager(BrowserType browser) {

		WebDriver driver = WebDriverFactory.createDriver(browser, CAPABILITIES.get());

		DRIVER.set(driver);
	}

	@Override
	public WebDriver getDriver() {
		return DRIVER.get();
	}

	@Override
	public Capabilities getDriverCapabilities() {
		return CAPABILITIES.get();
	}

	@Override
	public void setDriverCapabilities(Capabilities capabilities) {

		CAPABILITIES.set(capabilities);
	}

	public void quitDriver() {

		WebDriver driver = DRIVER.get();

		if (driver != null) {
			driver.quit();
			DRIVER.remove();
			CAPABILITIES.remove();
		}
	}
}
```

### 5. Usage Example

Chrome

```java
import org.openqa.selenium.chrome.ChromeOptions;
import com.framework.driver.*;

public class TestRunner {

	public static void main(String[] args) {

		ChromeOptions options = new ChromeOptions();
		options.addArguments("--start-maximized");
		options.addArguments("--incognito");

		DriverManager manager = new DriverManager(BrowserType.CHROME);

		manager.setDriverCapabilities(options);

		manager.getDriver().get("https://www.google.com");

		System.out.println(manager.getDriverCapabilities());

		manager.quitDriver();
	}
}
```


### Design Pattern Flow

```text
                DriverProvider (Interface)
                         │
                         ▼
                  DriverManager
                         │
                         ▼
                 WebDriverFactory
                         │
      ┌──────────┬──────────┬──────────┐
      ▼             ▼             ▼             ▼
 ChromeDriver  FirefoxDriver    EdgeDriver      xxxxxxxx
```

























Books to read:
- The prince
- The laws of human nature
- Dark psychology Secrets
- The Power of your subconscious mind
- 
