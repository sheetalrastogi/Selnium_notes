## JDBC Example - Processing Multiple ResultSets

Unlike a single result set, we use:	statement.execute();
and then iterate through all available results using: statement.getMoreResults();

```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;

public class CallableStmtMultipleResultSetExample {

	public static void main(String[] args) {

		String jdbcUrl = "jdbc:mysql://localhost:3306/DBName";

		String username = "username";
		String password = "password";

		String sql = "{call PRODUCT_MULTI_RS()}";

		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password);

				CallableStatement statement = connection.prepareCall(sql)) {

			boolean hasResults = statement.execute();

			int resultSetNumber = 1;

			while (hasResults) {

				try (ResultSet resultSet = statement.getResultSet()) {

					System.out.println("\nResult Set " + resultSetNumber++);

					while (resultSet.next()) {

						switch (resultSetNumber - 1) {

						case 1:
							System.out.println("NAME = " + resultSet.getString(1));
							break;

						case 2:
							System.out.println("Total Price = " + resultSet.getDouble(1));
							break;

						case 3:
							System.out.println("Max Price = " + resultSet.getDouble(1));

							System.out.println("Min Price = " + resultSet.getDouble(2));
							break;
						}
					}
				}

				hasResults = statement.getMoreResults();
			}

		} catch (SQLException e) {

			e.printStackTrace();
		}
	}
}
```

Output:

```text
Result Set 1
NAME = Pencil
NAME = Pen
NAME = Color Box

Result Set 2
Total Price = 47.60

Result Set 3
Max Price = 20.00
Min Price = 12.45
```


