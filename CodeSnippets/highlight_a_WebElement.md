## Highlight a WebElement with colored rectangle / circle / oval background

## 1. Highlight WebElement with Red Square Border

```java
public static void highlightElement(WebDriver driver, WebElement element) {
	JavascriptExecutor js = (JavascriptExecutor) driver;

	js.executeScript("arguments[0].style.border='3px solid red'", element);
}
```

## 2. Flash Element

```java
public static void flashElement(WebDriver driver, WebElement element) throws InterruptedException {

	JavascriptExecutor js = (JavascriptExecutor) driver;
	String originalColor = element.getCssValue("backgroundColor");

	for (int i = 0; i < 5; i++) {
		js.executeScript("arguments[0].style.background='yellow'", element);
		Thread.sleep(200);
		js.executeScript("arguments[0].style.background='" + originalColor + "'", element);
		Thread.sleep(200);
	}
}
```

## 3. Highlight with Red Oval

CSS border radius creates an oval effect.

```java
public static void highlightOval(WebDriver driver, WebElement element) {

	JavascriptExecutor js = (JavascriptExecutor) driver;

	js.executeScript("arguments[0].style.border='4px solid red';" + "arguments[0].style.borderRadius='50px';", element);
}

```

## 4. Highlight with Circle

Works well for buttons/icons having similar height and width.

```java
public static void highlightCircle(WebDriver driver, WebElement element) {

	JavascriptExecutor js = (JavascriptExecutor) driver;

	js.executeScript("arguments[0].style.border='4px solid red';" + "arguments[0].style.borderRadius='50%';", element);
}
```


**Other styles colors**:

- arguments[0].style.border='3px solid red';
- arguments[0].style.border='3px solid green';
- arguments[0].style.border='3px solid blue';


**remove style color:**

- arguments[0].style.border='';


## 5. Utility class

```java
public class ElementHighlighter {

	private ElementHighlighter() {
	}

	public static void highlight(WebDriver driver, WebElement element) {

		((JavascriptExecutor) driver).executeScript("arguments[0].style.border='3px solid red';", element);
	}

	public static void highlightGreen(WebDriver driver, WebElement element) {

		((JavascriptExecutor) driver).executeScript("arguments[0].style.border='3px solid green';", element);
	}

	public static void highlightBlue(WebDriver driver, WebElement element) {

		((JavascriptExecutor) driver).executeScript("arguments[0].style.border='3px solid blue';", element);
	}

	public static void removeHighlight(WebDriver driver, WebElement element) {

		((JavascriptExecutor) driver).executeScript("arguments[0].style.border='';", element);
	}
}
```

**Usage in Page Object Model(POM)**

```java
WebElement loginButton = driver.findElement(By.id("loginBtn"));

ElementHighlighter.highlight(driver, loginButton);

loginButton.click();
```
