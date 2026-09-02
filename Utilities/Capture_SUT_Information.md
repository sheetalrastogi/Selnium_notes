```java
package com.framework.utilities;

import java.awt.Dimension;
import java.awt.GraphicsEnvironment;
import java.awt.Toolkit;
import java.net.Inet4Address;
import java.net.InetAddress;
import java.net.NetworkInterface;
import java.net.SocketException;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Collections;
import java.util.Optional;

public final class SystemInfoUtil {

	private static final DateTimeFormatter DATE_TIME_FORMATTER = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

	private SystemInfoUtil() {
	}

	public static String getLocalTime() {
		return LocalDateTime.now().format(DATE_TIME_FORMATTER);
	}

	public static String getHostName() {
		try {
			return InetAddress.getLocalHost().getHostName();
		} catch (Exception e) {
			return "UNKNOWN_HOST";
		}
	}

	public static String getCanonicalHostName() {
		try {
			return InetAddress.getLocalHost().getCanonicalHostName();
		} catch (Exception e) {
			return "UNKNOWN_HOST";
		}
	}

	// Returns first non-loopback IPv4 address.
	public static Optional<String> getSystemIpAddress() {

		try {
			for (NetworkInterface network : Collections.list(NetworkInterface.getNetworkInterfaces())) {
				if (!network.isUp() || network.isLoopback() || network.isVirtual()) {
					continue;
				}

				for (InetAddress address : Collections.list(network.getInetAddresses())) {
					if (address instanceof Inet4Address && !address.isLoopbackAddress()) {
						return Optional.of(address.getHostAddress());
					}
				}
			}
		} catch (Exception ignored) {
		}
		return Optional.empty();
	}

	// Returns MAC address for the active network adapter.
	public static Optional<String> getMacAddress() {

		try {
			for (NetworkInterface network : Collections.list(NetworkInterface.getNetworkInterfaces())) {
				if (!network.isUp() || network.isLoopback() || network.isVirtual()) {
					continue;
				}

				byte[] mac = network.getHardwareAddress();
				if (mac == null || mac.length == 0) {
					continue;
				}

				StringBuilder builder = new StringBuilder();
				for (int i = 0; i < mac.length; i++) {
					builder.append(String.format("%02X%s", mac[i], (i < mac.length - 1) ? "-" : ""));
				}
				return Optional.of(builder.toString());
			}
		} catch (SocketException ignored) {
		}

		return Optional.empty();
	}

	// Safe for GUI environments.
	public static String getScreenResolution() {

		if (GraphicsEnvironment.isHeadless()) {
			return "HEADLESS";
		}

		Dimension size = Toolkit.getDefaultToolkit().getScreenSize();
		return (int) size.getWidth() + " x " + (int) size.getHeight();
	}

	public static String getOsName() {
		return System.getProperty("os.name");
	}

	public static String getOsVersion() {
		return System.getProperty("os.version");
	}

	public static String getJavaVersion() {
		return System.getProperty("java.version");
	}

	public static int getCpuCores() {
		return Runtime.getRuntime().availableProcessors();
	}
}

```
## Example usage

```java
		System.out.println("Time          : " + SystemInfoUtil.getLocalTime());
		System.out.println("Hostname      : " + SystemInfoUtil.getHostName());
		System.out.println("CanonicalName : " + SystemInfoUtil.getCanonicalHostName());
		System.out.println("IP Address    : " + SystemInfoUtil.getSystemIpAddress().orElse("NOT_FOUND"));
		System.out.println("MAC Address   : " + SystemInfoUtil.getMacAddress().orElse("NOT_FOUND"));
		System.out.println("Resolution    : " + SystemInfoUtil.getScreenResolution());
		System.out.println("OS Name       : " + SystemInfoUtil.getOsName());
		System.out.println("Java Version  : " + SystemInfoUtil.getJavaVersion());
		System.out.println("CPU Cores     : " + SystemInfoUtil.getCpuCores());
```

## Output:

```text
Time          : 2026-09-02 18:15:42
Hostname      : QE-WKS-01
CanonicalName : qe-wks-01.company.com
IP Address    : 10.20.30.40
MAC Address   : 00-1A-2B-3C-4D-5E
Resolution    : 1920 x 1080
OS Name       : Windows 11
Java Version  : 21.0.8
CPU Cores     : 16
```
Selenium Grid, Docker, or Jenkins framework

```text
driver.getCapabilities().getBrowserName();
driver.getCapabilities().getBrowserVersion();
driver.getCapabilities().getPlatformName();
```
