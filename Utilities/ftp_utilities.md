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

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.time.Duration;
import java.util.Objects;

public final class FtpHelper implements AutoCloseable {
	private final FTPClient client;
	private FtpHelper(FTPClient client) {
		this.client = client;
	}

	// Factory Method
	public static FtpHelper connect(String host, int port, String username, String password) throws IOException {
		Objects.requireNonNull(host, "Host cannot be null");
		FTPClient ftpClient = new FTPClient();
		try {
			ftpClient.connect(host, port);
			if (!ftpClient.login(username, password)) {
				throw new IOException("FTP authentication failed");
			}
			ftpClient.enterLocalPassiveMode();
			ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
			return new FtpHelper(ftpClient);
		} catch (Exception e) {
			disconnectQuietly(ftpClient);
			throw e;
		}
	}

	public void upload(Path localFile, String remoteFile) throws IOException {
		validateLocalFile(localFile);
		try (InputStream input = Files.newInputStream(localFile)) {
			if (!client.storeFile(remoteFile, input)) {
				throw buildFtpException("Upload failed for remote file: " + remoteFile);
			}
		}
	}

	public void download(String remoteFile, Path localFile) throws IOException {
		Files.createDirectories(localFile.getParent());
		try (OutputStream output = Files.newOutputStream(localFile)) {
			if (!client.retrieveFile(remoteFile, output)) {
				throw buildFtpException("Download failed for remote file: " + remoteFile);
			}
		}
	}

	public boolean fileExists(String remoteFile) throws IOException {
		FTPFile[] files = client.listFiles(remoteFile);
		return files != null && files.length > 0;
	}

	public void deleteFile(String remoteFile) throws IOException {
		if (!client.deleteFile(remoteFile)) {
			throw buildFtpException("Unable to delete remote file: " + remoteFile);
		}
	}

	public void cleanDirectory(String remoteDirectory) throws IOException {
		FTPFile[] files = client.listFiles(remoteDirectory);
		if (files == null) {
			return;
		}

		for (FTPFile file : files) {
			if (file.isFile()) {
				String remotePath = remoteDirectory + "/" + file.getName();
				deleteFile(remotePath);
			}
		}
	}

	public boolean waitForFile(String remoteFile, Duration timeout, Duration pollingInterval)
			throws InterruptedException, IOException {

		long endTime = System.currentTimeMillis() + timeout.toMillis();

		while (System.currentTimeMillis() < endTime) {
			if (fileExists(remoteFile)) {
				return true;
			}
			Thread.sleep(pollingInterval.toMillis());
		}
		return false;
	}

	public long getFileSize(String remoteFile) throws IOException {
		FTPFile[] files = client.listFiles(remoteFile);
		if (files == null || files.length == 0) {
			throw new IOException("Remote file not found: " + remoteFile);
		}
		return files[0].getSize();
	}

	public boolean isConnected() {
		return client.isConnected();
	}

	@Override
	public void close() throws IOException {
		try {
			if (client.isConnected()) {
				client.logout();
			}
		} finally {
			disconnectQuietly(client);
		}
	}

	private IOException buildFtpException(String message) {
		return new IOException(
				message + " | ReplyCode=" + client.getReplyCode() + " | ReplyMessage=" + client.getReplyString());
	}

	private static void validateLocalFile(Path file) {
		Objects.requireNonNull(file, "File path cannot be null");
		if (!Files.exists(file)) {
			throw new IllegalArgumentException("File does not exist: " + file);
		}
	}

	private static void disconnectQuietly(FTPClient client) {
		try {
			if (client != null && client.isConnected()) {
				client.disconnect();
			}
		} catch (Exception ignored) {
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


