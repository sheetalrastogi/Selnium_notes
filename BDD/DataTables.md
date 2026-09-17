##  Datatables conversion

In Cucumber, a Gherkin **DataTable** can be converted into multiple Java collection types depending on the structure of the table.


### 1. DataTable → List

**Feature**
```text
Scenario: Fruits List
  Given following fruits
    | Apple  |
    | Mango  |
    | Orange |
```

**Step Definition**
```java
@Given("following fruits")
public void following_fruits(DataTable dataTable) {

    List<String> fruits = dataTable.asList();

    fruits.forEach(System.out::println);
}
```
Output:
```text
Apple
Mango
Orange
```

### 2. DataTable → List<List>

**Feature**
```text
Scenario: User Details
  Given following users
    | John  | Admin |
    | Mike  | User  |
    | Sarah | Guest |
```

**Step Definition**

```java
@Given("following users")
public void following_users(DataTable dataTable) {

    List<List<String>> users = dataTable.asLists();

    for(List<String> row : users) {
        System.out.println(row.get(0) + " - " + row.get(1));
    }
}
```

Output:

```text
John - Admin
Mike - User
Sarah - Guest
```

### 3. DataTable → Map<String, String>

**Feature**

```text
Scenario: Login Details
  Given user credentials
    | username | admin123 |
    | password | pass123  |
```

**Step Definition**
```java
@Given("user credentials")
public void user_credentials(DataTable dataTable) {

    Map<String, String> credentials =
            dataTable.asMap(String.class, String.class);

    System.out.println(credentials.get("username"));
    System.out.println(credentials.get("password"));
}
```

Output:
```text
admin123
pass123
```

### 4. DataTable → List<Map<String,String>>

**Feature**
```text
Scenario: Multiple Users
  Given users information
    | username | password | role  |
    | admin    | admin123 | Admin |
    | john     | john123  | User  |
```

**Step Definition**
```java
@Given("users information")
public void users_information(DataTable dataTable) {

    List<Map<String,String>> users = dataTable.asMaps();

    for(Map<String,String> user : users) {

        System.out.println(user.get("username"));
        System.out.println(user.get("password"));
        System.out.println(user.get("role"));
    }
}
```

Output:

```text
admin
admin123
Admin

john
john123
User
```


### 5. DataTable → Map<String, List>

**Feature**
```text
Scenario: Department Employees
  Given departments
    | QA  | John  |
    | QA  | Mike  |
    | Dev | David |
    | Dev | Alex  |
```

**Step Definition**
```java
@Given("departments")
public void departments(DataTable dataTable) {

    Map<String, List<String>> map = new HashMap<>();

    for(List<String> row : dataTable.asLists()) {

        map.computeIfAbsent(row.get(0),
                k -> new ArrayList<>())
                .add(row.get(1));
    }

    System.out.println(map);
}
```
Output:

```text
{
 QA=[John, Mike],
 Dev=[David, Alex]
}

```

### 6. DataTable → Custom POJO

**Feature**
```text
Scenario: Customer Details
  Given customers
    | name  | age | city   |
    | John  | 30  | London |
    | Sarah | 25  | Paris  |
```

**Pojo**
```java
public class Customer {

    private String name;
    private int age;
    private String city;

    // getters/setters
}
```

**Step Definition**
```java
@Given("customers")
public void customers(DataTable dataTable) {

    List<Customer> customers = dataTable.asList(Customer.class);

    customers.forEach(c -> System.out.println(c.getName()));
}
```


### 7. DataTable → DefineType Registry / Transformer

**Feature**
```text
Scenario: Users
  Given users
    | username | password |
    | admin    | admin123 |
    | john     | john123  |
```
**Step Definition**
```java
@Given("users")
public void users(List<User> users) {

    users.forEach(u ->
            System.out.println(u.getUsername()));
}
```

**POJO**
```java
public class User {

    private String username;
    private String password;
}
```

**Transformer**
```java
@DataTableType
public User userTransformer(Map<String, String> row) {

    User user = new User();

    user.setUsername(row.get("username"));
    user.setPassword(row.get("password"));

    return user;
}
```


### 8. DataTable → Set

**Feature**
```text
Scenario: Roles
  Given available roles
    | Admin |
    | User  |
    | Admin |
```

**Step Definition**
```java
@Given("available roles")
public void available_roles(DataTable dataTable) {

    Set<String> roles =
            new HashSet<>(dataTable.asList());

    System.out.println(roles);
}
```

Output:
- [Admin, User]



### Quick Reference
```text
List<String>                  -> dataTable.asList()
List<List<String>>            -> dataTable.asLists()
Map<String, String>           -> dataTable.asMap()
List<Map<String, String>>     -> dataTable.asMaps()
Set<String>                   -> new HashSet<>(dataTable.asList())
List<POJO>                    -> dataTable.asList(MyPojo.class)
Custom Object Mapping         -> @DataTableType
Nested Structure              -> Manual conversion from asLists() or asMaps()
```
---
