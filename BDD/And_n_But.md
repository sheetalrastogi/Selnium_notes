## And and But usage in Gherkin

**And** and **But** are used to improve the readability of scenarios. They are syntactic replacements for Given, When, or Then and inherit the meaning of the preceding step.

**Example:   AND**

```text
Scenario: Successful login

  Given user is on the login page
  And user has a valid account
  And user is connected to the internet

  When user enters valid credentials

  Then user should be logged in
```


**Example:  But**

But is useful when expressing an exception or negative expectation.

```text
Scenario: Failed login

  Given user is on login page

  When user enters invalid password

  Then login should fail
  But user account should not be locked
```

**But with Given**

```text
Scenario: Apply discount

  Given customer is a premium member
  But customer subscription is expired

  When customer places an order

  Then discount should not be applied
```

**Example: And + But Together**

```text
Scenario: Money withdrawal

  Given account balance is 1000
  And ATM is operational

  When customer withdraws 500

  Then withdrawal should succeed
  And account balance should become 500
  But account should not be closed
```


### Step Definitions

No special step definitions are needed for And or But.

**Example**

```text
Given user is on login page
And user has a valid account
But user account is not locked
```

Can be implemented as follow:
```text
@Given("user is on login page")
public void userOnLoginPage() {}

@Given("user has a valid account")
public void validAccount() {}

@Given("user account is not locked")
public void accountNotLocked() {}
```

**Rule of thumb**

```text
And = "Also"
But = "However"
```

**Example**

```text
Then payment should be approved
And confirmation email should be sent
But loyalty points should not be awarded
```


