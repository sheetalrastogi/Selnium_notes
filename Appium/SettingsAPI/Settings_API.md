## Context APIs 

### Switch from Native App to WebView

- Native Login Screen → WebView Page

```java
// Get all contexts
Set<String> contexts = driver.getContextHandles();

for (String context : contexts) {
    if (context.contains("WEBVIEW")) {
        driver.context(context);
        break;
    }
}

System.out.println(driver.getContext());
```

- Switch Back to Native App

driver.switchTo().context("NATIVE_APP");



## Setting APIs

Settings API in Appium allows you to dynamically modify session-specific Appium driver behavior at runtime, similar to capabilities, but unlike capabilities these settings can be updated multiple times after the session has already started.

## Commonly Used Settings
| Setting | Purpose | Common Usage |
|----------|----------|--------------|
| ignoreUnimportantViews | Ignore non-essential views | Faster Android execution |
| waitForIdleTimeout | Wait for UI idle state | Performance tuning |
| allowInvisibleElements | Return hidden elements | Debugging |
| enableNotificationListener | Monitor notifications | Toast/Push validation |
| enableMultiWindows | Support multiple windows/WebViews | Hybrid apps |
| snapshotMaxDepth | Control hierarchy traversal depth | Deep UI trees |
| imageMatchThreshold | Image recognition confidence | Visual testing |
| elementResponseAttributes | Return additional attributes | Reporting/Debugging |
| shouldUseCompactResponses | Compact vs detailed responses | Framework diagnostics |

**Real-World Use Cases**
- Speed up Android execution by ignoring non-essential views.
- Capture Android toast messages.
- Improve WebView detection in hybrid apps.
- Tune image comparison thresholds for visual testing.
- Handle deeply nested iOS elements.
- Enable debug mode dynamically during failures.
- Apply different settings for local vs CI/CD runs.


## 1. Get Current Settings
```java
Map<String, Object> settings = driver.getSettings();
settings.forEach((key, value) -> System.out.println(key + " = " + value));
```

## 2. Update a Single Setting

```java
driver.setSetting(Setting.IGNORE_UNIMPORTANT_VIEWS, true);
```


## 3. Update Multiple Settings

```java
Map<String, Object> settings = Map.of(
    "ignoreUnimportantViews", true,
    "waitForIdleTimeout", 3000,
    "enableMultiWindows", true,
    "shouldUseCompactResponses", false,
    "elementResponseAttributes",
        "name,label,enabled"
);

driver.setSettings(settings);
```




