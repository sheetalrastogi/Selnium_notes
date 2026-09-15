## Log Filtering in Appium Java

Log Filtering in Appium allows you to control which logs are collected and displayed during test execution. This is particularly useful when:
- Reducing log noise in CI/CD pipelines
- Capturing only important Appium server logs
- Troubleshooting specific driver issues
- Improving log readability and performance

### 1. Appium Server Log Filtering Using Log Level

Start Appium Server:   	appium --log-level error
Output:  Only error messages are displayed.

Start Appium Server:	appium --log-level warn
Output: shows WARN and ERROR messages

Start Appium Server:  	appium --log-level info
Output: shows INFO, WARN & ERROR messages

Start Appium Server:	appium --log-level debug
Output:  shows all messages


### 2. Filter Device Logs (Android Logcat)

Retrieve logs and display only specific messages.

```java
LogEntries logEntries = driver.manage().logs().get("logcat");

for(LogEntry entry : logEntries) {
    if(entry.getMessage().contains("CRASH")) {
        System.out.println(entry.getMessage());
    }
}
```

### 2a. Filter Logs by Severity

```java
LogEntries logs = driver.manage().logs().get("logcat");

logs.getAll().stream()
        .filter(log ->
                log.getLevel().getName().equals("SEVERE"))
        .forEach(System.out::println);
```

### 2b. Capture Only Appium Errors

```java
LogEntries logs = driver.manage().logs().get("server");

logs.getAll()
    .stream()
    .filter(log ->
            log.getMessage().contains("[error]"))
    .forEach(log ->
            System.out.println(log.getMessage()));
```

### 3. Regex-Based Log Filtering

Useful when validating multiple error patterns.


```java
Pattern pattern = Pattern.compile("Exception|Crash|ANR");

LogEntries logs = driver.manage().logs().get("logcat");

logs.getAll().stream()
        .filter(log ->
                pattern.matcher(log.getMessage())
                       .find())
        .forEach(System.out::println);
```



### 4. Real-Time Log Filtering Using Logcat

Execute ADB and stream only relevant messages.

```java
ProcessBuilder builder =
        new ProcessBuilder(
                "adb",
                "logcat",
                "*:E");

Process process = builder.start();
```


**Summary**

Log Filtering in Appium helps you isolate meaningful information from Appium server logs, Android Logcat logs, iOS syslogs, and driver logs. In enterprise mobile automation frameworks, it is commonly used for:

- Automatic crash detection
- ANR monitoring
- Security exception tracking
- Performance troubleshooting
- CI/CD failure diagnostics
- Extent/Allure reporting integration



