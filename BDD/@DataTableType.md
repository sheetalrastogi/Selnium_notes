## @DataTableType 

It is a Cucumber feature that **automatically converts a Gherkin DataTable row into a Java POJO**. It makes step definitions cleaner and avoids manual Map<String,String> parsing.


### Without @DataTableType    Requires manual conversion of every row.

**Feature**
```text
Scenario: Create Users
  Given following users
    | username | password |
    | admin    | admin123 |
    | john     | john123  |
```
**Step Definition**
```java
@Given("following users")
public void followingUsers(DataTable dataTable) {

    List<Map<String, String>> users = dataTable.asMaps();

    for (Map<String, String> row : users) {

        User user = new User();
        user.setUsername(row.get("username"));
        user.setPassword(row.get("password"));

        System.out.println(user);
    }
}
```
---

### With @DataTableType 


**Step 1**: Create POJO
```java
public class User {
    private String username;
    private String password;

    // Constructor
    // All arguments constructor

    // getters / setters

    @Override
    public String toString() {
        return username + " : " + password;
    }
}
```

**Step 2**: Create DataTable Transformer   (No DataTable object needed.)

- Can be placed in a Hooks class or Step Definition class.

```java
import io.cucumber.java.DataTableType;

public class DataTableTransformers {

    @DataTableType
    public User userEntry(Map<String, String> row) {

        return new User(
                row.get("username"),
                row.get("password")
        );
    }
}
```

**Step 3**: Write Feature File

```text
Scenario: Create Users
  Given following users
    | username | password |
    | admin    | admin123 |
    | john     | john123  |
```

**Step 4**: Use List Directly
```text
@Given("following users")
public void followingUsers(List<User> users) {
    users.forEach(System.out::println);
}
```


Output
```text
admin : admin123
john : john123
```

---



### Example with Multiple Fields

**Feature**
```text
Scenario: Customer Details
  Given customers
    | id | name  | city   |
    | 1  | John  | London |
    | 2  | Sarah | Paris  |
```

**POJO**
```java
public class Customer {
    private int id;
    private String name;
    private String city;

    // getters + setters
}
```

**Transformer**
```java
@DataTableType
public Customer customerTransformer(Map<String, String> row) {
    Customer customer = new Customer();
    customer.setId(Integer.parseInt(row.get("id")));
    customer.setName(row.get("name"));
    customer.setCity(row.get("city"));

    return customer;
}
```

**Step Definition**
```java
@Given("customers")
public void customers(List<Customer> customers) {
    customers.forEach(customer ->
            System.out.println(customer.getName()));
}
```

---


### Using Enum Conversion

**Feature**
```text
Scenario: Users
  Given users
    | username | role  |
    | admin    | ADMIN |
    | john     | USER  |
```

**Enum**
```java
public enum Role {
    ADMIN,
    USER
}
```

**POJO**
```java
public class User {
    private String username;
    private Role role;

    // getters/setters
}
```

**Transformer**
```java
@DataTableType
public User transform(Map<String, String> row) {

    User user = new User();

    user.setUsername(row.get("username"));
    user.setRole(Role.valueOf(row.get("role")));

    return user;
}
```


**Summary**  

Use:

```text
@DataTableType
public User userTransformer(Map<String, String> row)

and then consume:

@Given("following users")
public void followingUsers(List<User> users)
```

This gives:

- Strong typing
- No column index dependency
- Cleaner step definitions
- Better IDE refactoring support
- Reusable domain objects across UI, API, and DB tests
- Easier maintenance in large BDD automation frameworks

---
