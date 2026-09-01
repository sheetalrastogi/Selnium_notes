## Instantiate AndroidDriver with basic capabilities

```java
import java.net.URL;

import org.openqa.selenium.remote.RemoteWebDriver;

import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.remote.options.UiAutomator2Options;

public class LaunchAndroidApp {

	public static void main(String[] args) throws Exception {

		UiAutomator2Options options = new UiAutomator2Options();

		options.setPlatformName("Android");

		// Android Version
		options.setPlatformVersion("14");

		// Device UDID
		options.setUdid("R58M123456A");

		// APK Location
		options.setApp("C:\\Apps\\MyApplication.apk");

		// Reset Options
		options.setNoReset(false);
		options.setFullReset(false);

		// Auto-switch to WebView if Hybrid App
		options.setAutoWebview(true);

		// Device Locale
		options.setLanguage("fr");
		options.setLocale("FR");

		// Device Orientation
		options.setOrientation(org.openqa.selenium.ScreenOrientation.LANDSCAPE);

		AndroidDriver driver = new AndroidDriver(new URL("http://127.0.0.1:4723"), options);

		System.out.println("Application Launched Successfully");

		System.out.println("Current Package : " + driver.getCurrentPackage());

		driver.quit();
	}
}

```
