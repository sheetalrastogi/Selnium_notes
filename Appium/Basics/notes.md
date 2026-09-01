## 1. How to Find Android UDID

ADB Command:
	adb devices

Output:
```text
	List of devices attached

	R58M123456A      device
	emulator-5554    device
```
here:  R58M1234...  is Udid of device.

UDID (Unique Device Identifier):  Appium uses the UDID capability to determine which device it should connect to and execute tests on when multiple devices are available.


## 2. Appium Capability: fullReset=true

For Android applications, Appium typically performs the following:
1. Uninstall existing application
2. Remove application data
3. Install fresh APK
4. Launch application
5. Execute test
6. Uninstall application after session 


**Verify app before uninstallation**

```java
String packageName = "com.myapp";

if (driver.isAppInstalled(packageName)) {
    driver.removeApp(packageName);
    System.out.println("Application removed.");
}
```


## 3. Wait for application launch (options.setAutoLaunch(true);)

By waiting For Application Package, immediately after session creation.

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(30));

wait.until(d -> ((AndroidDriver) d).getCurrentPackage().equals("com.myapp"));

OR

wait.until(d -> ((AndroidDriver) d).currentActivity().contains("MainActivity"));

```


## 4. appium:newCommandTimeout

The appium:newCommandTimeout capability specifies **how long Appium should keep a session alive when no new commands are received from the client (test script).**

When Is It Needed?:  
	- Application Takes Long Time to Process
	- Long Sleep Statements (Thread.sleep(Duration.ofMinutes(3).toMillis());)

Does Explicit Wait Affect It?
	- No
	WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(60));

	
example:

```java
 UiAutomator2Options options = new UiAutomator2Options();
 options.setCapability("appium:newCommandTimeout", 300);
```


## 5. Set Java Temporary Directory (Client side)

Set system variable:
	System.setProperty("java.io.tmpdir", "D:\\AutomationTemp");

Usage:
	File tempFile = File.createTempFile("appium",".tmp");
This effects:
	Java temp files
	Downloads
	Screenshots
	Custom framework artifacts

