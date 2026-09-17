## Example (singular)

**Feature**   This is simply an alias for **Scenario**.

```text
Rule: There can be only One

  Example: Only One -- More than one alive
    Given there are 3 ninjas
    ...
```

### Above is equivalent to:

```text
Scenario: Only One -- More than one alive
  Given there are 3 ninjas
  ...
```


## 2. Examples (plural)

```text
Scenario Outline: Login

  Given user enters "<username>"

Examples:
  | username |
  | admin    |
  | test     |
```

Following **structural Gherkin keywords** and do not require step definitions.

```text
Feature:
Rule:
Background:
Scenario:
Scenario Outline:
Examples:
Example:
```

Following **Executable Steps*** requires step definitions:

```text
Given ...
When ...
Then ...
And ...
But ...
```
