## S - Single Responsibility Principle (SRP)
	A class should have only one reason to change.

Following class violates SRP

```java
public class Employee {

    public void calculateSalary() {
        // salary logic
    }

    public void saveToDatabase() {
        // persistence logic
    }

    public void generateReport() {
        // reporting logic
    }
}
```

SRP Compliant:

```java
public class EmployeeSalaryService {
    public void calculateSalary() {}
}

public class EmployeeRepository {
    public void save() {}
}

public class EmployeeReportService {
    public void generateReport() {}
}
```


---
## O - Open/Closed Principle (OCP)

A classic Open/Closed Principle (OCP) implementation is where a class is:

- Open for Extension (new behavior can be added)
- Closed for Modification (existing code doesn't need to change)


**OCP Compliant Design**

### Option 1: Create Extension Point
public interface PaymentMethod {
    void pay(double amount);
}

- Implement Different Behaviors
public class CreditCardPayment implements PaymentMethod {
    @Override
    public void pay(double amount) {
        System.out.println("Credit Card Payment: " + amount);
    }
}

=> Similarly other implementations


### Option 2: Processor Depends on Abstraction

public class PaymentProcessor {
    public void processPayment(PaymentMethod paymentMethod,double amount) {
        paymentMethod.pay(amount);
    }
}

public class ApplePayPayment implements PaymentMethod {
    @Override
    public void pay(double amount) {
        System.out.println("Apple Pay Payment: " + amount);
    }
}

=> Similarly other extensions

Usage
public class TestApp {

    public static void main(String[] args) {
        PaymentProcessor processor = new PaymentProcessor();
        processor.processPayment(new CreditCardPayment(), 1000);
        processor.processPayment(new UpiPayment(), 500);
        processor.processPayment(new PaypalPayment(), 750);
    }
}

----

## L - Liskov Substitution Principle (LSP)

Derived classes must be substitutable for their base classes.

A child class should behave like its parent without breaking functionality.

Example (Violates LSP)

```java
class Bird {
    public void fly() {
        System.out.println("Flying");
    }
}

class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException();
    }
}
```
A penguin cannot fly, so substituting a Penguin for a Bird breaks behavior.

Example (Follows LSP)

```java
interface Bird {
}

interface FlyingBird extends Bird {
    void fly();
}

class Sparrow implements FlyingBird {

    public void fly() {
        System.out.println("Flying");
    }
}

class Penguin implements Bird {
}
```
Now substitution works correctly.


----

## I - Interface Segregation Principle (ISP)

Clients should not be forced to depend on methods they do not use.

Prefer many small interfaces over one large interface.

Example (Violates ISP):

```java
public interface Worker {
    void work();
    void eat();
    void sleep();
}
```

Example (Compliant ISP):

```java
public interface Workable {
    void work();
}
```

## D - Dependency Inversion Principle (DIP)

High-level modules should depend on abstractions, not concrete implementations.

Example (Violates DIP)

```java
public class NotificationService {

    private EmailSender sender =
            new EmailSender();

    public void notifyUser() {
        sender.send();
    }
}
```
NotificationService depends directly on EmailSender.


Example (Follows DIP)

```java
public interface MessageSender {
    void send();
}

public class EmailSender implements MessageSender {
    public void send() {
        System.out.println("Email Sent");
    }
}

public class NotificationService {

    private final MessageSender sender;

    public NotificationService(MessageSender sender) {
        this.sender = sender;
    }

    public void notifyUser() {
        sender.send();
    }
}
```

Usage:

```java
NotificationService service = new NotificationService(new EmailSender());
OR

NotificationService service = new NotificationService(new SmsSender());
```


### ## SOLID in Selenium/Appium Automation Framework
**SRP**  Each performs a single responsibility.
- DriverManager
- ConfigReader
- Page Objects
- ReportManager
- APIClient


**OCP** New drivers added without changing framework core.
- AndroidDriverFactory
- IOSDriverFactory
- WebDriverFactory
- SmartTVDriverFactory


**LSP** Any implementation can replace the interface.
- WebDriver
- ChromeDriver
- FirefoxDriver
- EdgeDriver
- RemoteWebDriver



**ISP** Small focused interfaces.
- ScreenshotProvider
- LoggingProvider
- VideoProvider
- NetworkProvider


**DIP** Tests depend on abstractions instead of concrete drivers.
```text
Test Classes
        ↓
DriverFactory Interface
        ↓
AndroidDriverFactory
IOSDriverFactory
```



**Quick Summary**

Principle	Meaning
S	One class → One responsibility
O	Extend behavior without modifying existing code
L	Child objects must safely replace parent objects
I	Prefer small, focused interfaces
D	Depend on abstractions, not implementations

Easy Memory Trick

SOLID =  Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion



