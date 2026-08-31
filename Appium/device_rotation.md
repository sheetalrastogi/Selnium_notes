## Rotate an app by 90 degree

```java
import io.appium.java_client.android.AndroidDriver;
import org.openqa.selenium.ScreenOrientation;

public class RotateAppExample {

	public static void main(String[] args) {

		AndroidDriver driver = DriverFactory.getDriver();

		try {

			System.out.println("Before Rotation: " + driver.getOrientation());

			// Rotate 90 degrees to Landscape
			driver.rotate(ScreenOrientation.LANDSCAPE);

			Thread.sleep(3000);

			System.out.println("After Rotation: " + driver.getOrientation());

		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			driver.quit();
		}
	}
}
```

**Rotate Back to Portrait**
```java
driver.rotate(ScreenOrientation.PORTRAIT);
```

**Validate rotation**

```java
driver.rotate(ScreenOrientation.LANDSCAPE);

assert driver.getOrientation() == ScreenOrientation.LANDSCAPE;
```

