## Detecting connection leaks for your application


The following program can be used to generate a large number of database connections and help identify potential connection pool leakage issues. In a properly implemented application, every database connection acquired from the pool should be returned to the pool by invoking close(). Failure to do so can eventually exhaust available connections, causing application slowdowns, timeouts, or outages.


```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class ConnectionLeakDetector {

	public static Connection getConnection() throws Exception {
		Connection ret = null;
		Class.forName(“com.microsoft.sqlserver.jdbc.SQLServerDriver”);
		ret = DriverManager.getConnection(“jdbc:sqlserver://192.168.152.1x;user=xx;password=xx;database=xx”);
		try {
			ret = new ro.kifs.diagnostic.Connection(ret);
		} catch (Exception x) {
			System.out.println(“EX registering conn in conn collection date: ” + x.getMessage());
			x.printStackTrace();
		}
		return ret;
	}

	public static void main(String[] args) throws Exception {
	
		for (int k = 0; k < 2; k++) {
			Connection conn = getConnection();
			Statement sta = conn.createStatement();
			String Sql = “select field1, field2 from table”;
			ResultSet rs = sta.executeQuery(Sql);
			while (rs.next()) {
				String cStatusID = rs.getString(1);
				String cStatus = rs.getString(2);
			}
		}
	}
}

```

Above code intentionally appears to create a database connection leak, because the following resources are never closed:
 - ResultSet rs
 - Statement sta
 - Connection conn

Once it is executed connections piled up at database level can be counted with following SQL Query:

```text 
SELECT DB_NAME(dbid) as DBName, COUNT(dbid) as NumberOfConnections, loginame as LoginName FROM sys.sysprocesses
WHERE dbid > 0 GROUP BY dbid, loginame
```
 
If number of connections do not drop after application is closed, we can assume a clear case of “Connection leakage” by application.
