## Transaction Management in JDBC


In database applications, especially in Selenium, API, and automation frameworks, it is common to perform multiple database operations as part of a single business transaction. If any operation fails, all preceding changes should be rolled back to maintain data consistency.

## Example 1: Commit or Rollback a Transaction

The following example inserts an employee record and then updates additional employee information. Both SQL statements are treated as a single transaction.


```java
import java.sql.Connection;
import java.sql.Date;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;

public class JDBCTransactionExample {

	private static final String INSERT_SQL = "INSERT INTO EMPLOYEE (EMP_ID, NAME, DOB) VALUES (?, ?, ?)";

	private static final String UPDATE_SQL = "UPDATE EMPLOYEE SET EMAIL = ?, DEPT = ? WHERE EMP_ID = ?";

	public static void main(String[] args) {

		String jdbcUrl = "jdbc:mysql://localhost:3306/Database";

		String username = "username";
		String password = "password";

		DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");

		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password)) {

			// Step 1: Disable Auto Commit

			connection.setAutoCommit(false);

			try (PreparedStatement insertStatement = connection.prepareStatement(INSERT_SQL);

					PreparedStatement updateStatement = connection.prepareStatement(UPDATE_SQL)) {

				// Insert Employee

				insertStatement.setInt(1, 1);
				insertStatement.setString(2, "Michael");

				insertStatement.setDate(3, new Date(dateFormat.parse("1995-07-01").getTime()));

				insertStatement.executeUpdate();

				// Update Employee

				updateStatement.setString(1, "michael@example.com");

				updateStatement.setString(2, "HR Department");

				updateStatement.setInt(3, 1);

				updateStatement.executeUpdate();

				// Step 2: Commit Transaction

				connection.commit();

				System.out.println("Transaction committed successfully.");

			} catch (SQLException | ParseException e) {

				System.out.println("Transaction is being rolled back.");

				connection.rollback();

				e.printStackTrace();
			}

		} catch (SQLException e) {

			e.printStackTrace();
		}
	}
}
```

Output:
Transaction committed successfully.

**Transaction flow**

```text
BEGIN TRANSACTION
       │
       ▼
INSERT RECORD
       │
       ▼
UPDATE RECORD
       │
       ▼
SUCCESS ?
   /      \
 YES      NO
 │          │
 ▼          ▼
COMMIT   ROLLBACK
```

## Example 2: Basic Commit / Rollback Pattern

The following simplified example demonstrates a common transaction pattern.

```java
String jdbcUrl = "jdbc:mysql://localhost:3306/Database";

String username = "username";
String password = "password";

Connection connection = null;

try {
	String connectionUrl = "jdbc:sqlserver://server:1433;databaseName=DBName";

	connection = DriverManager.getConnection(connectionUrl, "username", "password");

	connection.setAutoCommit(false);

	Statement statement = connection.createStatement();

	statement.executeUpdate(SQLQuery);

	// Commit on success

	connection.commit();

} catch (Exception e) {

	// Rollback on failure
	if (connection != null) {
		connection.rollback();
	}

} finally {
	if (connection != null) {
			connection.close();
	}
}

```

## Example 3: Using Savepoints

```java
import java.sql.Connection;
import java.sql.Date;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.Savepoint;
import java.sql.SQLException;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;

public class JDBCSavepointExample {

	private static final String INSERT_SQL = "INSERT INTO EMPLOYEE (EMP_ID, NAME, DOB) VALUES (?, ?, ?)";

	public static void main(String[] args) {

		String jdbcUrl = "jdbc:mysql://localhost:3306/DBName";

		String username = "username";
		String password = "password";

		DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");

		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password)) {

			connection.setAutoCommit(false);

			try (PreparedStatement statement = connection.prepareStatement(INSERT_SQL)) {

				// Employee 1

				statement.setInt(1, 1);
				statement.setString(2, "Michael");
				statement.setDate(3, new Date(dateFormat.parse("1995-07-01").getTime()));
				statement.executeUpdate();

				// Employee 2

				statement.setInt(1, 2);
				statement.setString(2, "Sunil");
				statement.setDate(3, new Date(dateFormat.parse("1988-03-22").getTime()));
				statement.executeUpdate();

				// Employee 3

				statement.setInt(1, 3);
				statement.setString(2, "Mike");
				statement.setDate(3, new Date(dateFormat.parse("1980-05-12").getTime()));
				statement.executeUpdate();

				// Create Savepoint

				Savepoint savepoint = connection.setSavepoint("EMPLOYEE_SAVEPOINT");

				// Employee 4

				statement.setInt(1, 4);
				statement.setString(2, "Manish");
				statement.setDate(3, new Date(dateFormat.parse("1992-01-21").getTime()));
				statement.executeUpdate();

				// Employee 5

				statement.setInt(1, 5);
				statement.setString(2, "Albert");
				statement.setDate(3, new Date(dateFormat.parse("1972-07-05").getTime()));
				statement.executeUpdate();

				// Rollback only Employee 4 and 5

				connection.rollback(savepoint);

				// Commit Employee 1, 2 and 3

				connection.commit();

				System.out.println("Transaction committed successfully.");

			} catch (SQLException | ParseException e) {

				System.out.println("Transaction is being rolled back.");

				connection.rollback();

				e.printStackTrace();
			}

		} catch (SQLException e) {

			e.printStackTrace();
		}
	}
}
```

Output:
Transaction committed successfully.

