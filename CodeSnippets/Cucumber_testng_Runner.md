## Cucumber + TestNG Runner in Selenium 4 Java 

TestNG runner for Cucumber TestNG Runner:  

```java
package test.main;

import io.cucumber.testng.AbstractTestNGCucumberTests;
import io.cucumber.testng.CucumberOptions;

@CucumberOptions(
        features = "Feature",
        glue = {"test.stepdef"},
        plugin = {
                "pretty",
                "json:target/report.json"
        }
        // ,dryRun = true
)
public class OnlineStoreIT extends AbstractTestNGCucumberTests {
}

```

## Parallel Execution Version

If you want TestNG to run Cucumber scenarios in parallel:

```java
package test.main;

import io.cucumber.testng.AbstractTestNGCucumberTests;
import io.cucumber.testng.CucumberOptions;
import org.testng.annotations.DataProvider;

@CucumberOptions(
        features = "Feature",
        glue = {"test.stepdef"},
        plugin = {
                "pretty",
                "json:target/report.json"
        }
)
public class OnlineStoreIT extends AbstractTestNGCucumberTests {

    @Override
    @DataProvider(parallel = true)
    public Object[][] scenarios() {
        return super.scenarios();
    }
}
```

**TestNG Suite** (testng.xml)
```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="Cucumber Suite">
    <test name="Online Store Tests">
        <classes>
            <class name="test.main.OnlineStoreIT"/>
        </classes>
    </test>
</suite>
```


**Required Maven Dependencies**
```xml
<dependencies>
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-java</artifactId>
        <version>7.31.0</version>
    </dependency>

    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-testng</artifactId>
        <version>7.31.0</version>
    </dependency>

    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.11.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```
