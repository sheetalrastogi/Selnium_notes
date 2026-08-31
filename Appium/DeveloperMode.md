## Developer mode 

Appium/Selenium cannot directly enable Android Developer Options on device (if Developer Options is currently disabled), because access to that setting itself requires user interaction, device-owner privileges, ADB authorization, or OEM-specific permissions.

However, if:

- USB debugging is already enabled, or
- You are running on an Emulator,

then you can automate navigation to the Developer Options screen and enable specific settings.

**Example 1: Open Android Developer Options Screen**

```java
import io.appium.java_client.android.AndroidDriver;

import java.util.Map;

public class OpenDeveloperOptions {

	public static void main(String[] args) {

		AndroidDriver driver = DriverFactory.getDriver();

		driver.executeScript("mobile: shell", Map.of("command", "am", "args",
				java.util.List.of("start", "-a", "android.settings.APPLICATION_DEVELOPMENT_SETTINGS")));

		System.out.println("Developer Options Opened");
	}
}
```

**Example 2: Enable "Stay Awake" in Developer Options**

```java
driver.findElement(AppiumBy.androidUIAutomator("new UiScrollable(new UiSelector().scrollable(true))" + ".scrollTextIntoView(\"Stay awake\")"));

driver.findElement(AppiumBy.androidUIAutomator("new UiSelector().text(\"Stay awake\")")).click();
```

