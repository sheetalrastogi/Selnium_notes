### Always-match  / First-match capabilities

- In Appium, capabilities are divided into:
	**alwaysMatch** → Capabilities that must always apply to every session.
	**firstMatch** → A list of alternative capability sets. Appium/WebDriver tries each entry and uses the first one that matches.

### Example 1: JSON Capability Structure

```json
{
  "capabilities": {
    "alwaysMatch": {
      "platformName": "Android",
      "appium:automationName": "UiAutomator2",
      "appium:newCommandTimeout": 300
    },
    "firstMatch": [
      {
        "appium:deviceName": "Pixel_9",
        "appium:platformVersion": "15"
      },
      {
        "appium:deviceName": "Samsung_S24",
        "appium:platformVersion": "14"
      }
    ]
  }
}
```

Resolution

Appium combines:	alwaysMatch + firstMatch[0]

Resulting capabilities:
```json
{
  "platformName": "Android",
  "appium:automationName": "UiAutomator2",
  "appium:newCommandTimeout": 300,
  "appium:deviceName": "Pixel_9",
  "appium:platformVersion": "15"
}
```

**If first option is unavailable**, Appium tries:   	alwaysMatch + firstMatch[1]


Example:

```java
import io.appium.java_client.android.AndroidDriver;
import org.openqa.selenium.MutableCapabilities;
import org.openqa.selenium.remote.RemoteWebDriver;

import java.net.URL;
import java.util.List;
import java.util.Map;

public class FirstMatchExample {

    public static void main(String[] args) throws Exception {

        MutableCapabilities alwaysMatch = new MutableCapabilities();
        alwaysMatch.setCapability("platformName", "Android");
        alwaysMatch.setCapability("appium:automationName", "UiAutomator2");

        Map<String, Object> pixelDevice = Map.of(
                "appium:deviceName", "Pixel_9",
                "appium:platformVersion", "15"
        );

        Map<String, Object> samsungDevice = Map.of(
                "appium:deviceName", "Samsung_S24",
                "appium:platformVersion", "14"
        );

        MutableCapabilities caps = new MutableCapabilities();
        caps.setCapability("alwaysMatch", alwaysMatch.asMap());
        caps.setCapability("firstMatch", List.of(pixelDevice, samsungDevice));

        RemoteWebDriver driver = new AndroidDriver(new URL("http://localhost:4723"), caps);

        driver.quit();
    }
}
```

## another approach

```java
List<Map<String, Object>> firstMatch = List.of(
        Map.of(
                "appium:deviceName", "iPhone 16",
                "appium:platformVersion", "18.0"
        ),

        Map.of(
                "appium:deviceName", "iPhone 15",
                "appium:platformVersion", "17.5"
        )
);
```

### What to put in "Always Match" capabilities:

```text
platformName
automationName
app package / bundle ID
newCommandTimeout
noReset
fullReset
```

### What to "Put in firstMatch" capabilities

```text
deviceName
platformVersion
udid
systemPort
wdaLocalPort
```



