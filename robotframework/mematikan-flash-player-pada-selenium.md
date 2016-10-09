# Mematikan plugin flash player pada selenium menggunakan Chrome

```
Open Chrome Without Flash
  [Arguments]         ${url}
  ${options}=         Evaluate                  sys.modules['selenium.webdriver'].ChromeOptions()     sys, selenium.webdriver
  ${disabled}=        Create List               Adobe Flash Player
  ${preferences}=     Create Dictionary         plugins.plugins_disabled=${disabled}
  Call Method         ${options}                add_experimental_option   prefs   ${preferences}
  Create WebDriver    Chrome                    chrome_options=${options}
  Go To               ${url}
```
