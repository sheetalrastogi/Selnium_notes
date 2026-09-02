## Identify the root cause of exception in Selenium

Consider following code snippet for “NoSuchElementException” condition in Selenium
```java
WebDriver driver;
driver = new FirefoxDriver();
driver.manage().window().maximize();
driver.get(“http://www.google.co.in”);
WebDriverWait wait = new WebDriverWait(driver, 20);
By addItem = By.name(“q”);
WebElement element = wait.until(ExpectedConditions.presenceOfElementLocated(addItem));

element.sendKeys(“Hello google”);

driver.findElement(By.xpath(“//input[@name=’btnK1′]”)).click();
```
**example output in case of invalid element**

```text
*** Element info: {Using=xpath, value=//input[@name=’btnK1′]}
at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
at org.openqa.selenium.remote.RemoteWebDriver.execute(RemoteWebDriver.java:647)
at org.testng.internal.MethodInvocationHelper.invokeMethod(MethodInvocationHelper.java:124)
...
...
at org.testng.remote.RemoteTestNG.main(RemoteTestNG.java:77)
Caused by: org.openqa.selenium.NoSuchElementException: Unable to locate element: {“method”:”xpath”,”selector”:”//input[@name=’btnK1′]”}
For documentation on this error, please visit: http://seleniumhq.org/exceptions/no_such_element.html
```
## While working with exception message, One can reduce the Stack trace and log relevant piece of information as follow:

```java
try{
WebDriver driver;
driver = new FirefoxDriver();
driver.manage().window().maximize();
driver.get(“http://www.google.co.in”);
WebDriverWait wait = new WebDriverWait(driver, 20);
By addItem = By.name(“q”);
WebElement element = wait.until(ExpectedConditions.presenceOfElementLocated(addItem));

element.sendKeys(“Hello google”);

driver.findElement(By.xpath(“//input[@name=’btnK1′]”)).click();
} catch (Exception e) {
while (e.getCause() != null)
e = (Exception) e.getCause();
System.out.println(“Root cause is ” + e.getMessage());
}
```
**Output**
Root cause is Unable to locate element: {“method”:”xpath”,”selector”:”//input[@name=’btnK1′]”}
For documentation on this error, please visit: http://seleniumhq.org/exceptions/no_such_element.html
