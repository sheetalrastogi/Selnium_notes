## Validating UI/API changes by traversing JDBC ResultSets 

In Selenium automation, database validation is often used to verify whether UI operations such as Create, Update, Delete, or Search have correctly persisted data in the backend database.

By default, a **JDBC ResultSet** is:

- Forward-only
- Read-only
- Non-scrollable

This means you can read records sequentially using next(), but you cannot move backward or jump to specific rows.

## For advanced validation scenarios, JDBC supports Scrollable and Updatable ResultSets, allowing test automation frameworks to:

- Navigate forward and backward
- Jump directly to specific records
- Insert records
- Update records
- Delete records
- Compare database states before and after Selenium actions

## ResultSet Types

JDBC supports the following ResultSet navigation modes.

ResultSet.TYPE_FORWARD_ONLY   -  ResultSet.TYPE_FORWARD_ONLY

- Cursor can move forward only.
- Default ResultSet type.
- Lowest memory overhead.

ResultSet.TYPE_SCROLL_INSENSITIVE - ResultSet.TYPE_SCROLL_INSENSITIVE

- Cursor can move forward and backward.
- Database changes made after ResultSet creation are not visible.


ResultSet.TYPE_SCROLL_SENSITIVE - ResultSet.TYPE_SCROLL_SENSITIVE

- Cursor can move forward and backward.
- Database changes made after ResultSet creation may be reflected.

Support depends on the JDBC driver and database vendor.


Working example:

## Sample Employee Table

For all examples:
```text
ID	NAME1	Jackie Chan
2	Tintin
3	Donald Duck
4	Roger S. Pressman
```

## Creating a Scrollable ResultSet

A standard Statement:

Statement stmt = connection.createStatement();

Creates:
TYPE_FORWARD_ONLY
CONCUR_READ_ONLY

To support scrolling and updates:

PreparedStatement stmt = connection.prepareStatement(
                sql,
                ResultSet.TYPE_SCROLL_INSENSITIVE,
                ResultSet.CONCUR_


## Example 1: Navigating Forward and Backward

The following example demonstrates movement to specific rows.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class ScrollableResultSetExample {

	public static void main(String[] args) {

		String jdbcUrl = "jdbc:sqlserver://server:1433;databaseName=DBName";

		String username = "username";
		String password = "password";

		String sql = "SELECT ID, NAME FROM EMPLOYEE";

		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password);

				PreparedStatement statement = connection.prepareStatement(sql, ResultSet.TYPE_SCROLL_INSENSITIVE,
						ResultSet.CONCUR_UPDATABLE);

				ResultSet resultSet = statement.executeQuery()) {

			// Move to 2nd row

			resultSet.absolute(2);

			System.out.println("ID : " + resultSet.getInt("ID") + "\tNAME : " + resultSet.getString("NAME"));

			// Move to 4th row

			resultSet.absolute(4);

			System.out.println("ID : " + resultSet.getInt("ID") + "\tNAME : " + resultSet.getString("NAME"));

			// First row

			resultSet.first();

			System.out.println("ID : " + resultSet.getInt("ID") + "\tNAME : " + resultSet.getString("NAME"));

			// Last row

			resultSet.last();

			System.out.println("ID : " + resultSet.getInt("ID") + "\tNAME : " + resultSet.getString("NAME"));

		} catch (SQLException e) {

			e.printStackTrace();
		}
	}
}
```

Output:

```text
ID : 2    NAME : Tintin
ID : 4    NAME : Roger S. Pressman
ID : 1    NAME : Jackie Chan
ID : 4    NAME : Roger S. Pressman
```


## Example 2: Insert a New Row Using ResultSet

An updatable ResultSet can insert data directly.

```java
try (ResultSet rs = statement.executeQuery()) {
    rs.moveToInsertRow();

    rs.updateInt("ID", 5);
    rs.updateString("NAME", "Tom Hardy");

    rs.insertRow();

    rs.moveToCurrentRow();
}
```

Output:
```text
ID : 1 NAME : Jackie Chan
ID : 2 NAME : Tintin
ID : 3 NAME : Donald Duck
ID : 4 NAME : Roger S. Pressman
ID : 5 NAME : Tom Hardy
```

## Example 3: Update a Row

The following updates the second employee.

```java
try (ResultSet rs = statement.executeQuery()) {

    rs.absolute(2);

    rs.updateString("NAME", "David");

    rs.updateRow();

    System.out.println(
            "ID : "
            + rs.getInt("ID")
            + "\tNAME : "
            + rs.getString("NAME"));
}
```

## Example 4: Delete Rows

Delete last row and second row.

```java
try (ResultSet rs = statement.executeQuery()) {
    rs.last();
    rs.deleteRow();
    rs.absolute(2);
    rs.deleteRow();
    rs.beforeFirst();

    while (rs.next()) {
        System.out.println(
                "ID : "
                + rs.getInt("ID")
                + "\tNAME : "
                + rs.getString("NAME"));
```



