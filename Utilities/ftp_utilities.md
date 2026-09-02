## Ftp Utilities (wrapper around Apache Commons Net FTPClient):

- Upload file
- Download file
- Verify file exists
- Delete file
- Cleanup directory
- Poll until file arrives


**Maven dependency**

```xml
<dependency>
    <groupId>commons-net</groupId>
    <artifactId>commons-net</artifactId>
    <version>3.11.1</version>
</dependency>
```


**Implementation - ftp functions**

```java
import org.apache.commons.net.ftp.FTP;
import org.apache.commons.net.ftp.FTPClient;
import org.apache.commons.net.ftp.FTPFile;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.file.Path;
import java.time.Duration;

public class FtpHelper implements AutoCloseable {

	private final FTPClient ftpClient;

	public FtpHelper(String host, int port, String username, String password) throws IOException {
		ftpClient = new FTPClient();

		ftpClient.connect(host, port);

		if (!ftpClient.login(username, password)) {
			throw new RuntimeException("FTP login failed");
		}

		ftpClient.enterLocalPassiveMode();
		ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
	}

	public void upload(Path localFile, String remoteFile) throws IOException {
		try (FileInputStream fis = new FileInputStream(localFile.toFile())) {
			if (!ftpClient.storeFile(remoteFile, fis)) {
				throw new RuntimeException("Upload failed: " + remoteFile);
			}
		}
	}

	public void download(String remoteFile, Path localFile) throws IOException {
		try (FileOutputStream fos = new FileOutputStream(localFile.toFile())) {
			if (!ftpClient.retrieveFile(remoteFile, fos)) {
				throw new RuntimeException("Download failed: " + remoteFile);
			}
		}
	}

	public boolean exists(String remoteFile) throws IOException {
		FTPFile[] files = ftpClient.listFiles(remoteFile);
		return files != null && files.length > 0;
	}

	public void delete(String remoteFile) throws IOException {
		ftpClient.deleteFile(remoteFile);
	}

	public void cleanupDirectory(String remoteDirectory) throws IOException {
		FTPFile[] files = ftpClient.listFiles(remoteDirectory);

		for (FTPFile file : files) {
			if (file.isFile()) {
				ftpClient.deleteFile(remoteDirectory + "/" + file.getName());
			}
		}
	}

	public boolean waitForFile(String remoteFile, Duration timeout, Duration pollingInterval) throws Exception {

		long endTime = System.currentTimeMillis() + timeout.toMillis();

		while (System.currentTimeMillis() < endTime) {

			if (exists(remoteFile)) {
				return true;
			}

			Thread.sleep(pollingInterval.toMillis());
		}

		return false;
	}

	@Override
	public void close() throws IOException {

		if (ftpClient.isConnected()) {
			ftpClient.logout();
			ftpClient.disconnect();
		}
	}
}
```


**Selenium Test usage**

```java

import java.nio.file.Paths;
import java.time.Duration;

public class FtpTest {

	public static void main(String[] args) throws Exception {

		try (FtpHelper ftp = new FtpHelper("ftp.myserver.com", 21, "testuser", "password")) {

			// Upload
			ftp.upload(Paths.get("target/report.pdf"), "/incoming/report.pdf");

			// Verify
			boolean exists = ftp.exists("/incoming/report.pdf");
			System.out.println("File Exists = " + exists);

			// Poll for generated file
			boolean arrived = ftp.waitForFile("/outgoing/result.csv", Duration.ofMinutes(2), Duration.ofSeconds(5));

			System.out.println("Result Available = " + arrived);

			// Download
			ftp.download("/outgoing/result.csv", Paths.get("downloads/result.csv"));

			// Delete
			ftp.delete("/incoming/report.pdf");

			// Cleanup folder
			ftp.cleanupDirectory("/temp");
		}
	}
}
```

**Selenium test case usage**

```java
@Test
public void verifyFileGeneratedOnFTP() throws Exception {

	driver.get("https://myapp.com");

	driver.findElement(By.id("generateReport")).click();

	try (FtpHelper ftp = new FtpHelper(host, 21, user, password)) {

		boolean available = ftp.waitForFile("/reports/dailyReport.csv", Duration.ofMinutes(3), Duration.ofSeconds(10));

		Assert.assertTrue(available, "Report was not generated on FTP");

		ftp.download("/reports/dailyReport.csv", Paths.get("downloads/dailyReport.csv"));
	}
}

```


