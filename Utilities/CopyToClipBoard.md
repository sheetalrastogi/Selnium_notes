## Utility method to copy from WebElement to Clipboard:

```java
import java.awt.Toolkit;
import java.awt.datatransfer.StringSelection;

import org.openqa.selenium.WebElement;

public class abc {
	public static void main(String[] args) {
	}

	public static void copyTextToClipboard(WebElement element) {
		String value = element.getAttribute("value");
		StringSelection selection = new StringSelection(value);
		Toolkit.getDefaultToolkit().getSystemClipboard().setContents(selection, null);
	}
}
```

**Usage**
```java
WebElement txtUserName = driver.findElement(By.id("username"));
copyTextToClipboard(txtUserName);
```



# Above utility is not suitable for Appium mobile automation because:
- Android has its own clipboard
- iOS has its own clipboard
- Remote Appium devices/emulators do not share the Java host clipboard
- Cloud providers (BrowserStack, SauceLabs, LambdaTest) run devices remotely


**Android/iOS Appium**
- Copy Text To Device Clipboard

String text="Hello Appium Clipboard";
driver.setClipboardText(text);

- Read Clipboard

String clipboardText = driver.getClipboardText();
System.out.println("Clipboard = " + clipboardText);


**Utility**

```java
import io.appium.java_client.AppiumDriver;
import org.openqa.selenium.WebElement;

public class ClipboardUtils {

    public static void copyElementTextToClipboard(AppiumDriver driver, WebElement element) {
        String text = element.getText();
        driver.setClipboardText(text);
        System.out.println("Copied to clipboard : " + text);
    }
}
```

**Usage**

```java
WebElement username = driver.findElement(By.id("username"));

ClipboardUtils.copyElementTextToClipboard(driver, username);
```


