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




