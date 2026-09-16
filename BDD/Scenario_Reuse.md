Source:    https://arxiv.org/pdf/2402.15928

# Scenario Reuse Approaches in Selenium + Cucumber + Java

For a **Selenium + Cucumber + Java** framework, there are multiple ways to implement scenario reuse. Some are recommended, while others should be used cautiously.

---

# Option 1: Reuse at Step Definition Level (Recommended)

This is the **Cucumber-recommended approach**.

## Reusable Feature

```gherkin
Scenario: Login
  Given User enters username
  And User enters password
  When User clicks login
  Then Dashboard should be displayed
```

## Reusable Step Definitions

```java
public class LoginSteps {

    @Given("User enters username")
    public void enterUsername() {
        loginPage.enterUsername("testuser");
    }

    @Given("User enters password")
    public void enterPassword() {
        loginPage.enterPassword("password");
    }

    @When("User clicks login")
    public void clickLogin() {
        loginPage.clickLogin();
    }

    @Then("Dashboard should be displayed")
    public void verifyDashboard() {
        dashboardPage.verifyDashboard();
    }
}
```

## Use the Same Steps Across Multiple Scenarios

```gherkin
Scenario: Search Product
  Given User enters username
  And User enters password
  When User clicks login
  Then Dashboard should be displayed
  When User searches for "Laptop"
  Then Search results are displayed
```

### Benefits

- ✅ Native Cucumber support
- ✅ Easy reporting
- ✅ Parallel execution friendly

---

# Option 2: Reusable Business Methods (Better Enterprise Approach)

Move workflow logic into a dedicated **Service/Workflow Layer**.

## LoginWorkflow

```java
public class LoginWorkflow {

    private LoginPage loginPage;

    public void login(String user, String password) {
        loginPage.enterUsername(user);
        loginPage.enterPassword(password);
        loginPage.clickLogin();
    }
}
```

## Step Definition

```java
public class LoginSteps {

    private LoginWorkflow loginWorkflow;

    @Given("User is logged in")
    public void loginUser() {
        loginWorkflow.login(
            "testuser",
            "password"
        );
    }
}
```

Now every feature can simply use:

```gherkin
Given User is logged in
```

### Benefits

- ✅ Reduces duplication
- ✅ Improves maintainability
- ✅ Aligns with enterprise framework design
- ✅ Encapsulates business workflows

This is the approach most mature Selenium frameworks implement.

---

# Option 3: Composite Steps

Create higher-level business-oriented steps.

## Feature

```gherkin
Given User is logged in
```

## Step Definition

```java
@Given("User is logged in")
public void userLoggedIn() {
    enterUsername();
    enterPassword();
    clickLogin();
    verifyDashboard();
}
```

## Internal Methods

```java
private void enterUsername() {}

private void enterPassword() {}

private void clickLogin() {}

private void verifyDashboard() {}
```

### Benefits

- ✅ Easy to implement
- ✅ Less duplication
- ✅ Cleaner feature files

---

# Option 4: Scenario Invocation (Paper Approach)

The paper introduces a function-like scenario reuse model.

## Feature

```gherkin
Scenario: Buy Product
  Given I call reusable scenario "Login"
  And I call reusable scenario "Search Product"
  And I call reusable scenario "Checkout"
```

## Step Definition

```java
@Given("I call reusable scenario {string}")
public void callReusableScenario(String scenarioName) {

    switch (scenarioName) {

        case "Login":
            reusableScenarioExecutor.executeLogin();
            break;

        case "Checkout":
            reusableScenarioExecutor.executeCheckout();
            break;
    }
}
```

## Scenario Executor

```java
public class ReusableScenarioExecutor {

    public void executeLogin() {
        loginWorkflow.login(
            "user",
            "password"
        );
    }

    public void executeCheckout() {
        checkoutWorkflow.checkout();
    }
}
```

## Usage

```gherkin
Scenario: Place Order
  Given I call reusable scenario "Login"
  And I call reusable scenario "Add To Cart"
  And I call reusable scenario "Checkout"
```

### Characteristics

- Treats scenarios like functions
- Useful for very large BDD suites
- Not a native Cucumber pattern
- Can make reporting harder to interpret

---

# Option 5: Dynamic Enum Approach (Paper)

Use enums for compile-time safety.

## Enum

```java
public enum ReusableScenarios {
    LOGIN,
    SEARCH_PRODUCT,
    CHECKOUT
}
```

## Step Definition

```java
@Given("I call scenario {word}")
public void callScenario(ReusableScenarios scenario) {

    switch (scenario) {

        case LOGIN:
            loginWorkflow.login();
            break;

        case CHECKOUT:
            checkoutWorkflow.checkout();
            break;
    }
}
```

## Usage

```gherkin
Given I call scenario LOGIN
And I call scenario CHECKOUT
```

### Benefits

- ✅ Compile-time safety
- ✅ IDE/VS Code autocomplete
- ✅ Fewer spelling mistakes
- ✅ Centralized scenario management

---

# Option 6: Feature Composition Using Background

Often the simplest solution.

## Background

```gherkin
Background:
  Given User enters username
  And User enters password
  When User clicks login
  Then Dashboard should be displayed
```

All scenarios automatically start from the logged-in state.

## Scenarios

```gherkin
Scenario: Search Product

Scenario: Add Product

Scenario: Checkout
```

### Benefits

- ✅ Built-in Cucumber support
- ✅ Minimal duplication
- ✅ Easy for common preconditions

---

# Enterprise QA Architect Recommendation

For large-scale **Selenium 4 + Cucumber + Java** frameworks:

```text
Feature Files
      ↓
Step Definitions
      ↓
Business Workflow Layer
      ↓
Page Objects
      ↓
WebDriver
```

## Recommended Workflow Structure

```text
Reusable Workflows
├─ LoginWorkflow
├─ SearchWorkflow
├─ CheckoutWorkflow
├─ CustomerWorkflow
└─ AdminWorkflow
```

## Resulting Gherkin

```gherkin
Given Customer is logged in
When Customer places order
Then Order should be successful
```

---

# Best Practice Summary

✅ Reuse **Step Definitions** where possible  
✅ Create **Workflow/Service classes** for business processes  
✅ Use **Composite Business
