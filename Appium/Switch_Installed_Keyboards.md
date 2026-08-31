keyboard layouts are controlled by the Android **Input Method Editor (IME)** installed on the device.

## Approach 1: Switch Input Method (IME)

**List installed keyboards**:
  adb shell ime list -s

Example output:
  com.google.android.inputmethod.latin/.LatinIME
  com.samsung.android.honeyboard/.service.HoneyBoardService
  com.google.android.inputmethod.japanese/.MozcService

**Selenium script to switch to Japanese keyboard**

```java
driver.executeScript("mobile: shell", Map.of("command", "ime", "args",
			List.of("set", "com.google.android.inputmethod.japanese/.MozcService")));
```

other examples:
			driver.executeScript("mobile: shell",
					Map.of("command", "ime", "args", List.of("set", "com.google.android.inputmethod.latin/.LatinIME")));


**Check if keyboard is displayed**

- Focus on a text field:
```java
			WebElement username = driver.findElement(AppiumBy.id("com.myapp:id/txtUsername"));
			username.click();
```
- Check keyboard visibility:

```java
System.out.println(driver.isKeyboardShown());
```

## // Check whether keyboard is displayed and hide it
```java
if (driver.isKeyboardShown()) {
    System.out.println("Keyboard is displayed. Closing keyboard...");
    driver.hideKeyboard();
} else {
    System.out.println("Keyboard is not displayed.");
}
```
