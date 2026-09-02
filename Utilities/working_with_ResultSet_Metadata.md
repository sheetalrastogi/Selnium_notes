## Working with ResultSet metada

ResultSetMetaData is a JDBC interface that provides metadata about the columns returned by a SQL query. Metadata is often described as "data about data", allowing applications to dynamically inspect the structure of query results without knowing the table schema in advance.

**Using ResultSetMetaData, you can retrieve information such as**:
- Number of columns returned by the query
- Column names
- Column labels (aliases)
- SQL data types
- Java class names
- Column display sizes
- Nullable status
- Auto-increment properties

This is particularly useful when developing:
- Generic database utilities
- Dynamic reporting tools
- Data export/import utilities
- Database validation frameworks

**Example Database Query**
- SELECT * FROM USERS;

Assume the USERS table contains:
```text
UID    NAME      DOB          EMAIL
---------------------------------------------
1      Joseph    1988-12-25   joe@example.com
2      Andrew    1975-05-20   andrew@example.com
```

## Example: Retrieving ResultSet Metadata

The following example demonstrates how to retrieve metadata and display query results.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;

public class ResultSetMetaDataExample {
	public static void main(String[] args) {
		String jdbcUrl = "jdbc:mysql://localhost:3306/DBName";
		String username = "username";
		String password = "password";
		String sql = "SELECT * FROM USERS";
		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password);
				PreparedStatement statement = connection.prepareStatement(sql);
				ResultSet resultSet = statement.executeQuery()) {

			ResultSetMetaData metaData = resultSet.getMetaData();
			System.out.println("----------- META DATA -----------");
			int columnCount = metaData.getColumnCount();
			for (int i = 1; i <= columnCount; i++) {
				String columnName = metaData.getColumnName(i);
				String columnType = metaData.getColumnTypeName(i);
				int displaySize = metaData.getColumnDisplaySize(i);
				System.out.println(
						"Column Name = " + columnName + "\t Type = " + columnType + "\t Size = " + displaySize);
			}

			System.out.println("\n----------- DATA -----------");
			while (resultSet.next()) {
				System.out.println("UID=" + resultSet.getString("UID"));
				System.out.println("NAME=" + resultSet.getString("NAME"));
				System.out.println("DOB=" + resultSet.getString("DOB"));
				System.out.println("EMAIL=" + resultSet.getString("EMAIL"));
				System.out.println();
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
}
```

**Output**

```text
----------- META DATA -----------

Column Name = UID      Type = INT       Size = 11
Column Name = NAME     Type = VARCHAR   Size = 45
Column Name = DOB      Type = DATE      Size = 10
Column Name = EMAIL    Type = VARCHAR   Size = 45

----------- DATA -----------

UID=1
NAME=Joseph
DOB=1988-12-25
EMAIL=joe@example.com

UID=2
NAME=Andrew
DOB=1975-05-20
EMAIL=andrew@example.com
```

Updated java code 

```java
			ResultSetMetaData metaData = resultSet.getMetaData();

			for (int i = 1; i <= metaData.getColumnCount(); i++) {

				System.out.println("Column Name : " + metaData.getColumnName(i));

				System.out.println("Column Label : " + metaData.getColumnLabel(i));

				System.out.println("Data Type : " + metaData.getColumnTypeName(i));

				System.out.println("Java Class : " + metaData.getColumnClassName(i));

				System.out.println("Nullable : " + metaData.isNullable(i));

				System.out.println("Auto Increment : " + metaData.isAutoIncrement(i));

				System.out.println("-----------------------");
			}
```

## Dynamic Result Printing

Instead of hardcoding column names, use metadata to print any query result dynamically.

```java
			ResultSetMetaData metaData = resultSet.getMetaData();

			int columnCount = metaData.getColumnCount();

			while (resultSet.next()) {

				for (int i = 1; i <= columnCount; i++) {

					System.out.print(metaData.getColumnName(i) + "=" + resultSet.getObject(i) + "\t");
				}

				System.out.println();
			}
```

