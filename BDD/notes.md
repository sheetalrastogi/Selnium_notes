## BDD Cucumber / Gherkin notes:

### 1. Gherkin Keywords and Colon Usage

| Category | Keyword | Colon (:) Required? | Example |
|-----------|----------|-------------------|---------|
| Section Keyword | Feature | ✅ Yes | `Feature: User Login` |
| Section Keyword | Rule | ✅ Yes | `Rule: Valid User Authentication` |
| Section Keyword | Background | ✅ Yes | `Background: Common Setup` |
| Section Keyword | Scenario | ✅ Yes | `Scenario: Successful Login` |
| Section Keyword | Scenario Outline | ✅ Yes | `Scenario Outline: Invalid Login Attempts` |
| Section Keyword | Examples | ✅ Yes | `Examples:` |
| Step Keyword | Given | ❌ No | `Given the user is on the login page` |
| Step Keyword | When | ❌ No | `When the user enters valid credentials` |
| Step Keyword | Then | ❌ No | `Then the dashboard should be displayed` |
| Step Keyword | And | ❌ No | `And the user clicks the Login button` |
| Step Keyword | But | ❌ No | `But the account is not locked` |
| Step Keyword | * | ❌ No | `* the cart contains 3 items` |

### Rule of Thumb

| Use Colon (:) | Do Not Use Colon (:) |
|--------------|----------------------|
| Feature | Given |
| Rule | When |
| Background | Then |
| Scenario | And |
| Scenario Outline | But |
| Examples | * |

---

### 2. Rule Keyword in Gherkin

The Rule keyword was introduced in Gherkin 6 to represent a single business rule that the feature must satisfy.

It helps organize large feature files by grouping related scenarios under a specific business rule.

**You do not implement Rule in Step Definitions.**

Rule is a **documentation and organization construct** in Gherkin. Cucumber does **not** create a separate Java annotation such as @Rule for step definitions.


**Without Rule**

```text
Feature: User Login

Scenario: Login with valid credentials
  Given User enters valid username and password
  When User clicks Login
  Then Dashboard is displayed

Scenario: Login with invalid password
  Given User enters valid username and invalid password
  When User clicks Login
  Then Error message is displayed

Scenario: Account should lock after 3 failed attempts
  Given User enters invalid password 3 times
  When User clicks Login
  Then Account should be locked
```

**With Rule**

```text
Feature: User Login

Rule: Registered users can access the application

  Scenario: Login with valid credentials
    Given User enters valid username and password
    When User clicks Login
    Then Dashboard is displayed

  Scenario: Login with invalid password
    Given User enters valid username and invalid password
    When User clicks Login
    Then Error message is displayed

Rule: Account must be protected against brute-force attacks

  Scenario: Account should lock after 3 failed attempts
    Given User enters invalid password 3 times
    When User clicks Login
    Then Account should be locked

  Scenario: Locked account cannot login
    Given User account is locked
    When User enters correct credentials
    Then Login should be denied
```

**Rule with Background**

```text
A Background can be defined inside a Rule.

Feature: Money Transfer

Rule: Transfer between active accounts

  Background:
    Given Source account is active
    And Destination account is active

  Scenario: Transfer valid amount
    When User transfers 100 dollars
    Then Transfer should succeed

  Scenario: Transfer exceeding balance
    When User transfers 10000 dollars
    Then Transfer should fail
```


**Hierarchy of a Feature File**

```text
Feature
 ├─ Rule
 │   ├─ Background (optional)
 │   ├─ Scenario
 │   └─ Scenario
 │
 ├─ Rule
 │   ├─ Scenario
 │   └─ Scenario
 │
 └─ Scenario
```
---

### 3. Scenario Outline in BDD Gherkin

```text
Feature: User Login

  Scenario Outline: Validate login with different credentials
    Given User is on the login page
    When User enters username "<username>" and password "<password>"
    And User clicks the Login button
    Then Login result should be "<result>"

    Examples:
      | username | password | result          |
      | admin    | admin123 | Login Success   |
      | admin    | wrong123 | Login Failed    |
      | testuser | test123  | Login Success   |
      | invalid  | invalid  | Login Failed    |
```

**Rule of Thumb**: Use Scenario when the test data is fixed. Use Scenario Outline when the same workflow must run with multiple sets of input data.

In standard Gherkin, an Examples section is always scoped to a single Scenario Outline; it cannot be shared among multiple scenarios.


---




