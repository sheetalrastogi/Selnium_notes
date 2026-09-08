## Execute TestNG tests in batches of 2 test cases

Example: 10 iterations → Run (1,2) together, then (3,4), then (5,6), etc.

You can achieve this using a DataProvider combined with parallel execution.

## Step 1: Execute Iterations in Batches of 2 Using DataProvider

**Test Class**

```java
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

public class BatchExecutionTest {
    @DataProvider(name = "batchData", parallel = true)
    public Object[][] batchData() {
        return new Object[][]{
                {1}, {2},
                {3}, {4},
                {5}, {6},
                {7}, {8},
                {9}, {10}
        };
    }

    @Test(dataProvider = "batchData")
    public void executeTest(Integer iteration) throws Exception {
        System.out.printf("Thread=%s Iteration=%d%n", Thread.currentThread().getName(), iteration);
        Thread.sleep(3000);
    }
}
```

## testng.xml

```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="BatchExecutionSuite">
    <test name="BatchOfTwo">
        <classes>
            <class name="tests.BatchExecutionTest"/>
        </classes>
    </test>
</suite>
```

## Surefire configuration

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>3.5.4</version>
    <configuration>
        <properties>
            <property>
                <name>dataproviderthreadcount</name>
                <value>2</value>
            </property>
        </properties>
    </configuration>
</plugin>
```

**Output**

```text
Thread=TestNG-PoolService-0 Iteration=1
Thread=TestNG-PoolService-1 Iteration=2

Thread=TestNG-PoolService-0 Iteration=3
Thread=TestNG-PoolService-1 Iteration=4

Thread=TestNG-PoolService-0 Iteration=5
Thread=TestNG-PoolService-1 Iteration=6
```
