# Generate Android locators 


In order to generate accurate Android element locators for Appium automation, provide one of the following application artifacts:

- activity_main.xml
- fragment_*.xml
- Jetpack Compose source code
- Android UIAutomator XML dump
- Appium Inspector page source or screenshot
- APK page source (driver.getPageSource() output)

These artifacts contain the UI hierarchy and element properties (such as resource-id, content-desc, text, and widget type) required to create reliable Appium locators, including:

```text
AppiumBy.id(...)
AppiumBy.accessibilityId(...)
AppiumBy.androidUIAutomator(...)
AppiumBy.xpath(...)
```




## Examples of What You Can Build From a Manifest - AndroidManifest.xml

AndroidManifest.xml defines application components (Activities, Services, Receivers, Permissions, etc.) and does not contain UI element definitions.


## Activity Verification

```java
String currentActivity = ((AndroidDriver)driver).currentActivity();

Assert.assertEquals(currentActivity, ".MainActivity");
```


## Start Activity Directly

```java
driver.executeScript("mobile: startActivity", Map.of("intent","com.example.app/.MainActivity"));

```

## Verify Application Package


```java
String packageName = ((AndroidDriver) driver).getCurrentPackage();

Assert.assertEquals(packageName,"com.example.app");
```

