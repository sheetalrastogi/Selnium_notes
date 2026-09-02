## Calling a Stored Procedure from Java Using JDBC

Java provides the **CallableStatement** interface to execute database stored procedures.

## Sample Stored Procedure 

```text
DELIMITER $$

CREATE PROCEDURE GetEmployeeName (
    IN emp_id INT
)
BEGIN
    SELECT employee_name
    FROM employees
    WHERE employee_id = emp_id;
END$$

DELIMITER ;
```

## Java Code to call above Stored Procedure

```java
import java.sql.*;

public class StoredProcedureExample {

	public static void main(String[] args) {

		String url = "jdbc:mysql://localhost:3306/mydb";

		String username = "root";
		String password = "password";

		try (Connection connection = DriverManager.getConnection(url, username, password)) {

			CallableStatement stmt = connection.prepareCall("{call GetEmployeeName(?)}");

			stmt.setInt(1, 101);

			ResultSet rs = stmt.executeQuery();

			while (rs.next()) {
				System.out.println(rs.getString("employee_name"));
			}

		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

## 2. Stored Procedure with IN Parameters

```text
CREATE PROCEDURE AddEmployee(
    IN emp_name VARCHAR(100),
    IN emp_salary DECIMAL(10,2)
)
BEGIN
    INSERT INTO employees
    (employee_name, salary)
    VALUES
    (emp_name, emp_salary);
END;
```

**Java code changes**

```java
CallableStatement stmt = connection.prepareCall("{call AddEmployee(?, ?)}");
stmt.setString(1, "John");
stmt.setDouble(2, 50000.00);
stmt.execute();
```

## 3. Stored Procedure with OUT Parameter

```text
CREATE PROCEDURE GetEmployeeCount(
    OUT total INT
)
BEGIN
    SELECT COUNT(*)
    INTO total
    FROM employees;
END;
```

**Java code changes**

```java
CallableStatement stmt = connection.prepareCall("{call GetEmployeeCount(?)}");
stmt.registerOutParameter(1, Types.INTEGER);
stmt.execute();
int count = stmt.getInt(1);
System.out.println("Employee Count = " + count);
```

## 4. Stored Procedure with IN and OUT Parameters

```text
CREATE PROCEDURE GetSalary(
    IN emp_id INT,
    OUT emp_salary DECIMAL(10,2)
)
BEGIN
    SELECT salary
    INTO emp_salary
    FROM employees
    WHERE employee_id = emp_id;
END;
```


```java
CallableStatement stmt = connection.prepareCall("{call GetSalary(?, ?)}");
stmt.setInt(1, 101);
stmt.registerOutParameter(2, Types.DOUBLE);
stmt.execute();
double salary = stmt.getDouble(2);
System.out.println("Salary = " + salary);
```

## 5. Stored Procedure Returning Result Set

```text
CREATE PROCEDURE GetEmployees()
BEGIN
    SELECT *
    FROM employees;
END;
```

```java
CallableStatement stmt = connection.prepareCall("{call GetEmployees()}");

ResultSet rs = stmt.executeQuery();
while (rs.next()) {
	System.out.println(rs.getInt("employee_id") + " " + rs.getString("employee_name"));
}
```

