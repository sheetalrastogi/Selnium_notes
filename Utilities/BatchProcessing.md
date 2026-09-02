## JDBC Batch Processing in Java

When inserting or updating a large number of database records, executing one SQL statement at a time can be inefficient. JDBC provides Batch Processing, which allows multiple SQL statements to be grouped together and sent to the database in a single request.

**Batch processing improves**
- Performance
- Network efficiency
- Transaction management
- Database throughput

The key methods used are:
- PreparedStatement.addBatch();
- PreparedStatement.executeBatch();

addBatch() adds the current SQL statement to a batch.
executeBatch() sends all batched statements to the database for execution.

## Example 1: Insert 200 Records in a Single Batch

The following example inserts 200 records into the BOOKS table using a single batch transaction.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class JDBCBatchInsertExample {

	private static final String INSERT_SQL = "INSERT INTO BOOKS (NAME, AUTHOR) VALUES (?, ?)";

	public static void main(String[] args) {

		String jdbcUrl = "jdbc:mysql://localhost:3306/DBName";
		String username = "username";
		String password = "password";

		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password)) {

			connection.setAutoCommit(false);

			try (PreparedStatement statement = connection.prepareStatement(INSERT_SQL)) {

				for (int i = 1; i <= 200; i++) {

					statement.setString(1, "Java");
					statement.setString(2, "Sunil Singh");

					// Add current statement to batch
					statement.addBatch();
				}

				// Execute all 200 records together
				statement.executeBatch();

				connection.commit();

				System.out.println("Transaction committed successfully.");

			} catch (SQLException e) {

				System.out.println("Error occurred. Rolling back transaction.");

				connection.rollback();
				throw e;
			}

		} catch (SQLException e) {

			e.printStackTrace();
		}
	}
}
```

How it works:
```text
Loop 200 Times
      │
      ▼
addBatch()
      │
      ▼
executeBatch()
      │
      ▼
commit()
```

All 200 records remain in memory until executeBatch() is called.

**Limitation of Large Batches**
 - When processing thousands or millions of records, storing the entire batch in memory may lead to:

	 - java.lang.OutOfMemoryError

because all statements are accumulated before execution.

For large datasets, it is recommended to execute smaller batches repeatedly.

## Example 2: Execute Records in Chunks of 10

Instead of sending all records in a single batch, divide them into smaller chunks.

**Benefits**:
- Lower memory consumption
- Better scalability
- Easier recovery in case of failures
- Reduced risk of OutOfMemoryError


```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class JDBCBatchChunkExample {

	private static final String INSERT_SQL = "INSERT INTO BOOKS (NAME, AUTHOR) VALUES (?, ?)";

	private static final int TOTAL_RECORDS = 100;

	private static final int BATCH_SIZE = 10;

	public static void main(String[] args) {

		String jdbcUrl = "jdbc:mysql://localhost:3306/DBName";
		String username = "username";
		String password = "password";

		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password)) {

			connection.setAutoCommit(false);

			try (PreparedStatement statement = connection.prepareStatement(INSERT_SQL)) {

				int batchCounter = 1;

				for (int i = 1; i <= TOTAL_RECORDS; i++) {

					statement.setString(1, "Java");
					statement.setString(2, "Sunil Singh");

					statement.addBatch();

					if (i % BATCH_SIZE == 0) {

						statement.executeBatch();

						connection.commit();

						statement.clearBatch();

						System.out.println("Batch " + batchCounter++ + " executed successfully");
					}
				}

				// Process remaining records if any

				statement.executeBatch();

				connection.commit();

				System.out.println("Final batch executed successfully");

			} catch (SQLException e) {

				System.out.println("Error occurred. Rolling back transaction.");

				connection.rollback();

				throw e;
			}

		} catch (SQLException e) {

			e.printStackTrace();
		}
	}
}
```

Output:

```text
Batch 1 executed successfully
Batch 2 executed successfully
Batch 3 executed successfully
Batch 4 executed successfully
Batch 5 executed successfully
Batch 6 executed successfully
Batch 7 executed successfully
Batch 8 executed successfully
Batch 9 executed successfully
Batch 10 executed successfully
Final batch executed successfully
```
