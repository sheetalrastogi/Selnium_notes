In Selenium 4 Java, **browser zoom** can be changed using Javascript and CDP.

1. Using JavaScript (Browser Zoom)

```java
JavascriptExecutor js = (JavascriptExecutor) driver;

// Zoom out to 80%
js.executeScript("document.body.style.zoom='80%'");

// Zoom in to 125%
js.executeScript("document.body.style.zoom='125%'");

// Reset zoom
js.executeScript("document.body.style.zoom='100%'");
```

**Utility method**

```java
	public static void setZoom(WebDriver driver, int percentage) {
		((JavascriptExecutor) driver).executeScript("document.body.style.zoom='" + percentage + "%'");
	}
```

Usage:
```java
setZoom(driver, 75);
setZoom(driver, 100);
setZoom(driver, 150);
```

## 2. Using Chrome DevTools Protocol (CDP)

More reliable for Chromium browsers.

```java
ChromeDriver driver = new ChromeDriver();

driver.executeCdpCommand(
        "Emulation.setPageScaleFactor",
        Map.of("pageScaleFactor", 1.25)
);
```

where:  
```text
1.0  = 100%
0.8  = 80%
1.25 = 125%
1.5  = 150%
```

**Usage**
```java
driver.executeCdpCommand(
        "Emulation.setPageScaleFactor",
        Map.of("pageScaleFactor", 0.75)
);
```
