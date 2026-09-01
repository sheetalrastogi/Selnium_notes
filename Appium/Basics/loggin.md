## 1. Appium Server and Client Logging in Selenium 4 and Appium

Capturing logs is essential for troubleshooting test failures, application crashes, device issues, and Appium server communication problems. A comprehensive logging strategy should include:

- Appium Server Logs (Server-side)
- Device Logs (Logcat) (Android device/emulator)
- Client/Test Execution Logs (Selenium/Appium framework logs)

## 1a. Appium Server Logging

Appium server logs capture:
- Session creation
- Capability negotiation
- Driver commands
- Appium errors
- Device communication
- Driver-specific logs (UiAutomator2, XCUITest)

How to capture Appium server logs:

**Option 1**: Start Appium Server with Log Redirection
```text
appium --log C:\Logs\appium.log
```
**Option 2**:Start Appium Server Programmatically

```java
import java.io.File;

import io.appium.java_client.service.local.AppiumDriverLocalService;
import io.appium.java_client.service.local.AppiumServiceBuilder;

public class AppiumServerManager {

	public static void main(String[] args) {

		AppiumDriverLocalService service = new AppiumServiceBuilder().withLogFile(new File("target/appium.log"))
				.build();
		service.start();
		System.out.println("Appium Server Started");
		// Execute Tests
		service.stop();
	}
}
```

## 1b. Appium Client Drivers / Device Logs with Logcat

Android Logcat captures:
- Application crashes
- ANR (Application Not Responding)
- Security exceptions
- Runtime exceptions
- Network failures
- Application lifecycle events


**Option 1**: Capture Logcat During Execution

```java
String logs = driver.executeScript("mobile: shell", java.util.Map.of("command", "logcat", "args", java.util.List.of("-d"))).toString();

System.out.println(logs);

```

**Option 2**: Capture Device Logs Using Selenium Logs API

- Print Device Logs to Console

```java
LogEntries entries = driver.manage().logs().get("logcat");

for (LogEntry entry : entries) {
	System.out.println(entry.getTimestamp() + " : " + entry.getMessage());
}
```


## 1c. Client-Side Logging (Automation Framework Logs)

Client logs capture:
- Test execution steps
- Locator actions
- Verification details
- Custom framework messages
- Exception information

**Sample framework logger**

```java
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

public class LoginTest {
	private static final Logger logger = LogManager.getLogger(LoginTest.class);
	public static void main(String[] args) {
		logger.info("Launching application");
		logger.info("Entering username");
		logger.info("Clicking Login button");
		logger.info("Login successful");
	}
}
```

- **Recommended Logging Strategy**
- Appium Server Log
	- Session Creation
	- Capabilities
	- Driver Commands
	- Server Errors

- Android Device Log
	- Application Logs
	- Crash Information
	- ANR Events
	- Runtime Exceptions

- Test Framework Log
	- Test Steps
	- Assertions
	- Business Actions
	- Framework Events

**Recommended Log Folder Structure**

```text
target/
│
├── appium.log
├── logcat.txt
├── device.log
├── test-execution.log
│
├── screenshots/
│
└── reports/
```
This approach provides complete visibility into Appium Server activity, Android device behavior, and test execution flow, making troubleshooting significantly easier in Selenium 4 + Appium automation frameworks.
