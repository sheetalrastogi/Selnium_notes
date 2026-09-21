```java
import io.appium.java_client.AppiumBy;
import io.appium.java_client.android.AndroidDriver;
import java.util.List;
import java.util.Map;

public class InstalledAppsFinder {
    public static void main(String[] args) {
        AndroidDriver driver = null;
        try {
            // Returns all installed packages
            Map<String, Object> response = driver.executeScript(
                    "mobile: shell",
                    Map.of(
                            "command", "pm",
                            "args", List.of("list", "packages", "-f")
                    )
            );

            String output = (String) response.get("stdout");
            System.out.println("===== Installed Applications =====");

            for (String line : output.split("\n")) {
                // Example:  package:/system/app/Calendar/Calendar.apk=com.android.calendar
                String packageName = line.substring(line.indexOf("=") + 1);
                String apkPath = line.substring(
                        line.indexOf(":") + 1,
                        line.indexOf("="));
                System.out.println("Package : " + packageName);
                System.out.println("APK Path: " + apkPath);
                System.out.println("--------------------------------");
            }

        } finally {
            if (driver != null) {
                driver.quit();
            }
        }
    }
}
```

**Common options**

```text
pm list packages        # all packages
pm list packages -3     # user-installed apps
pm list packages -s     # system apps
pm list packages -f     # include apk path
pm list packages -d     # disabled apps
pm list packages -e     # enabled apps
pm list packages -u     # uninstalled packages retained for users
```

## Note:
- iOS does not provide a public API to enumerate all installed apps due to Apple security restrictions. On iOS, Appium can generally interact only with the app under test (or apps explicitly launched by bundle ID on supported setups).
- 
