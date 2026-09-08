## Troubleshooting older Selenium/ChromeDriver issues

for troubleshooting older Selenium/ChromeDriver issues, especially errors such as:

```text
chrome automation extension crashed
unknown error: Chrome failed to start
disconnected: not connected to DevTools
session not created
```
The main idea is to verify ChromeDriver and Chrome browser compatibility and collect additional diagnostic logs.

## Pre-requisites

1. Why ChromeDriver Version Matters

ChromeDriver acts as a bridge between Selenium and Chrome.

- If ChromeDriver and Chrome versions are incompatible, Selenium may fail with errors such as:

SessionNotCreatedException

This version of ChromeDriver only supports Chrome version XX
Current browser version is YY

2. Finding ChromeDriver Version

chromedriver.exe -v   or chromedriver.exe --version

3. Purpose of Chrome Command-Line Flags

The article launches Chrome manually with numerous flags:	

chrome.exe --disable-background-networking
           --enable-automation
           --enable-logging
           --remote-debugging-port=12046


4. Important Chrome Flags

- Automation mode:  --enable-automation
- Logging:   --enable-logging
- Verbose logging:	--verbose
- Log File:		--log-path=chromedriver.log
- Remote Debugging:		--remote-debugging-port=12046
- Fresh User Profile:	--user-data-dir=C:\Temp\ChromeProfile
- Ignore certificates:	--ignore-certificate-errors


5. launching Chrome without extensions:  --disable-default-apps

Chrome extensions can interfere with Selenium by:

✓ Consuming memory
✓ Blocking automation
✓ Injecting JavaScript
✓ Causing browser crashes


6. Collecting diagnostic logs:   chrome.exe --verbose --log-path=verboseLogging.log


## 7. Selenium Equivalent:

```java
ChromeOptions options = new ChromeOptions();

options.addArguments("--enable-logging");
options.addArguments("--verbose");
options.addArguments("--remote-debugging-port=9222");
options.addArguments("--user-data-dir=C:\\Temp\\ChromeProfile");

WebDriver driver = new ChromeDriver(options);
```


### Launch Chrome in Automation Mode with Logging Enabled

```cmd
chrome.exe "https://www.google.com" ^
  --enable-automation ^
  --enable-logging ^
  --log-level=0 ^
  --remote-debugging-port=12046 ^
  --safebrowsing-disable-auto-update ^
  --test-type=webdriver ^
  --user-data-dir="C:\Users\[my username]\AppData\Local\Temp"
```

### Single-Line Version

```cmd
chrome.exe "https://www.google.com" --enable-automation --enable-logging --log-level=0 --remote-debugging-port=12046 --safebrowsing-disable-auto-update --test-type=webdriver --user-data-dir="C:\Users\[my username]\AppData\Local\Temp"
```

### Command-Line Arguments Explained

| Argument | Purpose |
|----------|---------|
| `--enable-automation` | Runs Chrome in automation mode. |
| `--enable-logging` | Enables Chrome logging. |
| `--log-level=0` | Sets logging to the most verbose level. |
| `--remote-debugging-port=12046` | Opens Chrome DevTools Protocol (CDP) endpoint on port 12046. |
| `--safebrowsing-disable-auto-update` | Disables Safe Browsing auto-updates. |
| `--test-type=webdriver` | Indicates browser is being used for WebDriver testing. |
| `--user-data-dir=<path>` | Uses a dedicated Chrome profile directory for testing. |

### Example with Full Chrome Path

```cmd
"C:\Program Files\Google\Chrome\Application\chrome.exe" "https://www.google.com" --enable-automation --enable-logging --log-level=0 --remote-debugging-port=12046 --safebrowsing-disable-auto-update --test-type=webdriver --user-data-dir="C:\Users\[my username]\AppData\Local\Temp"
```


---

## Launch Chrome with Extensive Automation and Debug Logging

### Multi-Line Version

```cmd
chrome.exe ^
  --disable-background-networking ^
  --disable-client-side-phishing-detection ^
  --disable-default-apps ^
  --disable-hang-monitor ^
  --disable-popup-blocking ^
  --disable-prompt-on-repost ^
  --disable-sync ^
  --disable-web-resources ^
  --enable-automation ^
  --enable-logging ^
  --ignore-certificate-errors ^
  --log-level=0 ^
  --metrics-recording-only ^
  --no-first-run ^
  --password-store=basic ^
  --remote-debugging-port=12046 ^
  --safebrowsing-disable-auto-update ^
  --test-type=webdriver ^
  --use-mock-keychain ^
  --user-data-dir="C:\Users\[my username]\AppData\Local\Temp" ^
  --verbose ^
  --log-path=chromedriver.log
```

### Single-Line Version

```cmd
chrome.exe --disable-background-networking --disable-client-side-phishing-detection --disable-default-apps --disable-hang-monitor --disable-popup-blocking --disable-prompt-on-repost --disable-sync --disable-web-resources --enable-automation --enable-logging --ignore-certificate-errors --log-level=0 --metrics-recording-only --no-first-run --password-store=basic --remote-debugging-port=12046 --safebrowsing-disable-auto-update --test-type=webdriver --use-mock-keychain --user-data-dir="C:\Users\[my username]\AppData\Local\Temp" --verbose --log-path=chromedriver.log
```

## Command-Line Arguments Explained

| Argument | Purpose |
|-----------|----------|
| `--disable-background-networking` | Disables background network services. |
| `--disable-client-side-phishing-detection` | Disables phishing detection checks. |
| `--disable-default-apps` | Prevents loading default Chrome apps. |
| `--disable-hang-monitor` | Disables browser hang monitoring. |
| `--disable-popup-blocking` | Allows popups without browser intervention. |
| `--disable-prompt-on-repost` | Suppresses repost confirmation dialogs. |
| `--disable-sync` | Disables Chrome account synchronization. |
| `--disable-web-resources` | Reduces background web resource loading. |
| `--enable-automation` | Indicates browser is running under automation. |
| `--enable-logging` | Enables Chrome logging. |
| `--ignore-certificate-errors` | Ignores SSL/TLS certificate errors. |
| `--log-level=0` | Enables maximum logging detail. |
| `--metrics-recording-only` | Records metrics without reporting them. |
| `--no-first-run` | Skips Chrome first-run setup screens. |
| `--password-store=basic` | Uses a basic password store implementation. |
| `--remote-debugging-port=12046` | Exposes Chrome DevTools on port 12046. |
| `--safebrowsing-disable-auto-update` | Disables Safe Browsing updates. |
| `--test-type=webdriver` | Indicates the browser is being used for WebDriver testing. |
| `--use-mock-keychain` | Uses a mock keychain for credential storage. |
| `--user-data-dir=<path>` | Uses a dedicated Chrome profile directory. |
| `--verbose` | Enables verbose logging output. |
| `--log-path=chromedriver.log` | Writes detailed logs to `chromedriver.log`. |

## Common Usage

This command is typically used for:

- Diagnosing **"Chrome Automation Extension Crashed"** issues
- Troubleshooting Chrome startup failures
- Collecting detailed browser logs
- Testing with a clean browser profile
- Enabling Chrome DevTools debugging
- Reproducing Selenium browser launch issues outside WebDriver

---

