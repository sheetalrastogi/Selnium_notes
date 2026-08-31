Common Android Settings Intents

An Intent is an Android messaging object used to request an action from another application component such as an **Activity**, **Service**, or **Broadcast Receiver**. 

In mobile automation, Intents are commonly used to 
- launch Activities directly, 
- test deep links, 
- trigger broadcasts, and 
- validate inter-application communication without navigating through the application's UI flow.

Some of Intents for "Android Settings" 

```text
// General Settings
android.settings.SETTINGS

// WiFi
android.settings.WIFI_SETTINGS

// Bluetooth
android.settings.BLUETOOTH_SETTINGS

// Airplane Mode
android.settings.AIRPLANE_MODE_SETTINGS

// Accessibility
android.settings.ACCESSIBILITY_SETTINGS

// Location
android.settings.LOCATION_SOURCE_SETTINGS

// Security
android.settings.SECURITY_SETTINGS

// Application Settings
android.settings.APPLICATION_SETTINGS

// Notification Settings
android.settings.APP_NOTIFICATION_SETTINGS

// Display Settings
android.settings.DISPLAY_SETTINGS
```



Below is a simple Selenium 4 + Appium Java example that sequentially opens various Android Settings screens using Android Intents and pauses for a few seconds so you can visually verify each screen.


```java
package utilities;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

import io.appium.java_client.android.AndroidDriver;

public final class AndroidSettingsUtil {

	private AndroidSettingsUtil() {
	}

	public static void openSettings(AndroidDriver driver, String action) {

		Map<String, Object> args = new HashMap<>();

		args.put("command", "am");
		args.put("args", List.of("start", "-a", action));

		driver.executeScript("mobile: shell", args);
	}
}
```


**AndroidSettingsDemo usage**

```java
package tests;

import io.appium.java_client.android.AndroidDriver;
import utilities.AndroidSettingsUtil;

public class AndroidSettingsDemo {

	public static void main(String[] args) throws Exception {

		AndroidDriver driver = DriverFactory.createAndroidDriver();

		try {

			String[] settingsScreens = { "android.settings.SETTINGS", "android.settings.WIFI_SETTINGS",
					"android.settings.BLUETOOTH_SETTINGS", "android.settings.AIRPLANE_MODE_SETTINGS",
					"android.settings.ACCESSIBILITY_SETTINGS", "android.settings.LOCATION_SOURCE_SETTINGS",
					"android.settings.SECURITY_SETTINGS", "android.settings.APPLICATION_SETTINGS",
					"android.settings.APP_NOTIFICATION_SETTINGS", "android.settings.DISPLAY_SETTINGS" };

			for (String action : settingsScreens) {

				System.out.println("Opening : " + action);

				AndroidSettingsUtil.openSettings(driver, action);

				Thread.sleep(3000);

				System.out.println("Current Screen = " + driver.currentActivity());
			}

		} finally {
			driver.quit();
		}
	}
}
```


why useful:

Appium Example: Launch Activity via Intent


```java
driver.executeScript("mobile: startActivity", Map.of("intent", "com.myapp/.MainActivity"));

```
This is much faster for following launch activities, as because it opens the desired Activity directly.

```text
Launch App
↓
Splash Screen
↓
Home Screen
↓
Menu
↓
Target Screen
```


