### Asynchronous JavaScript delay of approximately 500 milliseconds

```java
private void waitForLoad(WebDriver driver) {
	long start = System.currentTimeMillis();
	((JavascriptExecutor) driver).executeAsyncScript("window.setTimeout(arguments[arguments.length - 1], 500);");
	System.out.println("Wait time over :" + (System.currentTimeMillis() - start));
}
```

### Another Way to Wait for Page Load

```java
new WebDriverWait(driver, Duration.ofSeconds(30))
    .until(webDriver ->
        ((JavascriptExecutor) webDriver)
            .executeScript("return document.readyState")
            .equals("complete"));
```
