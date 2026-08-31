## Appium switching between open apps

eg. Launch App-A, switch to App-B, perform actions, and switch back to App-A


```java
import io.appium.java_client.AppiumBy;
import io.appium.java_client.android.AndroidDriver;
import org.openqa.selenium.WebElement;

public class AppSwitchExample {

	public static void main(String[] args) {

		AndroidDriver driver = DriverFactory.getDriver();

		try {

			String appA = "com.sender.app";
			String appB = "com.receiver.app";

			// Launch App-A
			driver.activateApp(appA);

			System.out.println("Current App: " + driver.getCurrentPackage());

			// Perform some action in App-A
			WebElement sendButton = driver.findElement(AppiumBy.id("com.sender.app:id/btnSend"));

			sendButton.click();

			// Switch to App-B
			driver.activateApp(appB);

			System.out.println("Current App: " + driver.getCurrentPackage());

			// Perform some action in App-B
			WebElement messageLabel = driver.findElement(AppiumBy.id("com.receiver.app:id/txtMessage"));

			System.out.println("Message Received: " + messageLabel.getText());

			// Switch back to App-A
			driver.activateApp(appA);

			System.out.println("Switched Back To: " + driver.getCurrentPackage());

		} finally {

			driver.quit();
		}
	}
}
```


This approach is generally useful for scenarios like:

```text
This approach is commonly used for:

Banking App ↔ OTP App
Main App ↔ Gmail
Main App ↔ Chrome
Main App ↔ Settings
Main App ↔ Authenticator App
Main App ↔ Notification Handler App
```

