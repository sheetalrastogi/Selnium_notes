## Event Timing API in Appium

The **Event Timing API** in Appium is a feature that collects performance timing metrics for commands executed during a session. It helps you measure how long Appium operations take, such as finding elements, clicking buttons, launching apps, switching contexts, etc.

Instead of relying on manual timers (System.currentTimeMillis()), Appium can automatically record session-level timing information and return it through the session details.


## Why Use Event Timing API?

- It helps answer questions such as:
	- How long did app launch take?
	- Which Appium command is slow?
	- How much time is spent finding elements?
	- Is a test failing because of application latency or automation latency?
	- Are performance characteristics different across devices?

**This is useful for:**
- Mobile test performance analysis
- CI/CD trend monitoring
- Device benchmarking
- Root cause analysis of slow tests

## How to Enable Event Timing API

Enable it when creating the driver session.  eg.

```java
UiAutomator2Options options = new UiAutomator2Options();

options.setDeviceName("Pixel_8");
options.setPlatformName("Android");

// Enable Event Timing API
options.setCapability("eventTimings", true);

AndroidDriver driver = new AndroidDriver(new URL("http://127.0.0.1:4723"), options);
```


Example usages (Execute Some Actions):

```java
driver.findElement(AppiumBy.accessibilityId("Login")).click();

driver.findElement(AppiumBy.id("username")).sendKeys("testuser");

driver.findElement(AppiumBy.id("password")).sendKeys("password");
```

Appium automatically records timing data for these commands.


##  Retrieve Event Timing Data

### Method 1: Get Session Details

```java
Map<String, Object> sessionDetails = driver.getSessionDetails();

System.out.println(sessionDetails);
```

Output:

```xml
{
  "events": {
    "newSessionRequested": [
      1694630000000
    ],
    "newSessionStarted": [
      1694630001500
    ],
    "commands": [
      {
        "cmd": "findElement",
        "startTime": 1694630003000,
        "endTime": 1694630003200
      },
      {
        "cmd": "click",
        "startTime": 1694630003300,
        "endTime": 1694630003400
      }
    ]
  }
}
```

### 2. Extract Command Duration

```java
Map<String, Object> details = driver.getSessionDetails();

Map<String, Object> events = (Map<String, Object>) details.get("events");

List<Map<String, Object>> commands = (List<Map<String, Object>>) events.get("commands");

for (Map<String, Object> command : commands) {

    String cmd = command.get("cmd").toString();

    long start = Long.parseLong(command.get("startTime").toString());

    long end = Long.parseLong(command.get("endTime").toString());

    long duration = end - start;

    System.out.println(cmd + " : " + duration + " ms");
}
```

Output:

```text
findElement : 200 ms
click : 100 ms
sendKeys : 350 ms
```

### 3. Common Events Captured

- Session Events:
	- newSessionRequested
	- newSessionStarted
	- quitSessionRequested
	- quitSessionFinished

- Command Events:
	- findElement
	- findElements
	- click
	- sendKeys
	- getPageSource
	- terminateApp
	- activateApp
	- executeScript

Example:  Measuring App Launch Time

```java
long start = System.currentTimeMillis();

driver.activateApp("com.demo.app");

long end = System.currentTimeMillis();

System.out.println("Launch Time = " + (end - start) + " ms");
```





