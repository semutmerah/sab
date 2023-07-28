### install webdriver-manager
```
pip3 install webdriver-manager
```

### buat custom keyword untuk memanggil webdriver-manager
```
# webdrivermanager.py
from webdriver_manager.chrome import ChromeDriverManager
from webdriver_manager.firefox import GeckoDriverManager

def get_driver_path_with_browser(browser_name):
    if browser_name.lower() == 'chrome':
        driver_path = ChromeDriverManager().install()
    elif browser_name.lower() == 'firefox':
        driver_path = GeckoDriverManager().install()
    print(driver_path)
    return driver_path
```

### pakai custom keywordnya ketika open browser
```
*** Setting ***
Documentation         Global resources
Library               SeleniumLibrary        timeout=10s    run_on_failure=Capture Page Screenshot     screenshot_root_directory=${SCREENSHOT_PATH}
Library               ../lib/webdrivermanager.py

*** Variables ***
${SCREENSHOT_PATH}        screenshots
${HOST}                   https://www.google.com
${BROWSER}                chrome
${BROWSER_WIDTH}          1366
${BROWSER_HEIGHT}         768

*** Keywords ***
Open Chrome Browser
  [Arguments]         ${url}    ${web_browser}=${BROWSER}
  ${driverPath}=      Get Driver Path With Browser    ${BROWSER}
  &{desiredCapabilities}  Create Dictionary   pageLoadStrategy=eager
  Open Browser        ${url}    ${web_browser}        options=add_argument("lang=id");add_argument("--disable-web-security");add_argument("--allow-running-insecure-content");add_argument("--disable-dev-shm-usage");add_argument("--incognito")    desired_capabilities=&{desiredCapabilities}    executable_path=${driverPath}
  Set Window Size        ${BROWSER_WIDTH}        ${BROWSER_HEIGHT}
```
