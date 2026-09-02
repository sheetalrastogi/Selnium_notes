## Save Image File into Database Using JDBC

Many enterprise applications need to store user profile pictures, scanned documents, signatures, screenshots, or other binary files directly in a database. JDBC provides support for storing and retrieving binary data using a BLOB (Binary Large Object) column.

To store an image file in a database:
- Use PreparedStatement#setBinaryStream() to write image data into a BLOB column.
- Use ResultSet#getBinaryStream() to retrieve image data from a BLOB column.
- Store the image as an InputStream to avoid loading the entire file into memory.


## Database Table Structure

The following MySQL table stores user information along with a profile image.

```text
CREATE TABLE USER_PROFILE
(
    USER_ID INT NOT NULL AUTO_INCREMENT,
    NAME VARCHAR(100) NOT NULL,
    IMAGE BLOB,
    PRIMARY KEY (USER_ID)
);
```

## Example: Save an Image File into Database

The following JDBC program inserts an image file into the USER_PROFILE table.

```java
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class ImageUploadExample {

	private static final String INSERT_SQL = "INSERT INTO USER_PROFILE(NAME, IMAGE) VALUES (?, ?)";

	public static void main(String[] args) {

		String jdbcUrl = "jdbc:mysql://localhost:3306/DBName";

		String username = "username";
		String password = "password";

		File imageFile = new File("sample.jpg");

		try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password);

				FileInputStream imageStream = new FileInputStream(imageFile);

				PreparedStatement statement = connection.prepareStatement(INSERT_SQL)) {

			statement.setString(1, "Mike");

			statement.setBinaryStream(2, imageStream, imageFile.length());

			int rowsInserted = statement.executeUpdate();

			if (rowsInserted > 0) {
				System.out.println("Image saved successfully.");
			}

		} catch (SQLException | IOException e) {

			e.printStackTrace();
		}
	}
}
```

**How it works**

```text
Image File
      │
      ▼
FileInputStream
      │
      ▼
setBinaryStream()
      │
      ▼
BLOB Column
      │
      ▼
Database
```

**Key statement**

```java
statement.setBinaryStream(2, imageStream, imageFile.length());
```

This converts the image into a binary stream and stores it in the database BLOB column.


## Reading an Image Back from Database

The following example retrieves an image from the database and writes it back to a file.

```java
import java.io.FileOutputStream;
import java.io.InputStream;
import java.sql.*;

public class ImageDownloadExample {

	private static final String SELECT_SQL = "SELECT IMAGE FROM USER_PROFILE WHERE USER_ID = ?";

	public static void main(String[] args) {

		try (Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/DBName", "username",
				"password");

				PreparedStatement statement = connection.prepareStatement(SELECT_SQL)) {

			statement.setInt(1, 1);

			ResultSet rs = statement.executeQuery();

			if (rs.next()) {

				InputStream inputStream = rs.getBinaryStream("IMAGE");

				FileOutputStream outputStream = new FileOutputStream("downloaded.jpg");

				byte[] buffer = new byte[4096];
				int bytesRead;

				while ((bytesRead = inputStream.read(buffer)) != -1) {

					outputStream.write(buffer, 0, bytesRead);
				}

				outputStream.close();

				System.out.println("Image downloaded successfully.");
			}

		} catch (Exception e) {

			e.printStackTrace();
		}
	}
}
```
