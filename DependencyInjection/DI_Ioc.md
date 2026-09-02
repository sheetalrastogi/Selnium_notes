**Dependency Injection** is a design technique where an object's dependencies are **provided from outside rather than created internally**. This leads to **loose coupling**, **better testability**, and **easier maintenance**. For enterprise Java applications, frameworks such as **Spring**, **PicoContainer**, **NanoContainer**, and **Guice** simplify dependency management and enable scalable application architectures.


## Why is it called Inversion of Control (IoC)?

Dependency Injection was originally known as Inversion of Control (IoC).

**Traditional control flow**

```text
Object
   │
   ├── Creates Dependency A
   ├── Creates Dependency B
   └── Uses Dependencies
```

**IoC / DI Control Flow**

```text
Application Container
        │
        ├── Creates Dependency A
        ├── Creates Dependency B
        └── Injects them into Object
```

The object no longer controls the creation of its dependencies.

This demonstrates the **Hollywood Principle**:

**"Don't call us, we'll call you."**

Instead of searching for dependencies, they are supplied when needed.


Assume:

Assume you depend on two or more objects to create a functional representation of an "Add to Cart" implementation.

Traditionally, this can be achieved by:

Creating instances of all dependent objects manually and using them in your implementation.

```text
ShoppingCartService cartService = new ShoppingCartService();
InventoryService inventoryService = new InventoryService();
PricingService pricingService = new PricingService();

AddToCartHandler handler = new AddToCartHandler(cartService, inventoryService, pricingService);

```

```java
public class AddToCartService {

    private InventoryService inventoryService = new InventoryService();

    private PricingService pricingService = new PricingService();

    public void addItem(String productId) {
        inventoryService.validateStock(productId);
        pricingService.calculatePrice(productId);
    }
}
```

**Problems**
- Tight coupling
- Difficult unit testing
- Hard to replace implementations
- Violates Single Responsibility Principle


## Types of Dependency Injection

**1. Constructor Injection (Recommended)**

```java
public class OrderService {

    private final PaymentService paymentService;

    public OrderService(
            PaymentService paymentService) {

        this.paymentService = paymentService;
    }
}
```

**2. Setter Injection**

```java
public class OrderService {
    private PaymentService paymentService;

    public void setPaymentService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

**3. Field Injection (Spring)**

```java
@Service
public class OrderService {

    @Autowired
    private PaymentService paymentService;
}
```


## Dependency Injection Example

Instead of creating dependencies internally, inject them externally.


```java
public class AddToCartService {

	private final InventoryService inventoryService;
	private final PricingService pricingService;

	public AddToCartService(InventoryService inventoryService, PricingService pricingService) {
		this.inventoryService = inventoryService;
		this.pricingService = pricingService;
	}

	public void addItem(String productId) {
		inventoryService.validateStock(productId);
		pricingService.calculatePrice(productId);
	}
}
```

Usage:

```text
InventoryService inventoryService = new InventoryService();

PricingService pricingService = new PricingService();

AddToCartService service = new AddToCartService(inventoryService, pricingService);

service.addItem("P1001");
```


**Advantages of Dependency Injection**

- Loose Coupling
- Easier Unit Testing
- Better Maintainability
- Higher Flexibility
- Improved Reusability
- Separation of Concerns
- Easier Refactoring
- Easier Mocking and Stubbing
- Supports SOLID Principles
- Reduces Object Creation Responsibility

