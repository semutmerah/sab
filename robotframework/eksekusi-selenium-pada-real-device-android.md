# Eksekusi Selenium2Library pada real device android via Chrome Browser

```
*** Settings ***
Documentation     A resource for global
Library           Selenium2Library      timeout=15


*** Variable ***
${COMMAND_EXECUTOR}   http://localhost:4723/wd/hub
${BROWSER}            Chrome
${PLATFORM_NAME}      Android
${UDID}               01b15d0795d50b10

*** Keywords ***
Open Android Browser
  [Documentation]     To open android default browser (not chrome) and go to provided URL
  [Arguments]         ${url}
  ${capabilities}=    Create Dictionary   browserName=${BROWSER}    platformName=${PLATFORM_NAME} udid=${UDID}   deviceName=${PLATFORM_NAME}
  Create Webdriver    Remote  command_executor=${COMMAND_EXECUTOR}    desired_capabilities=${capabilities}
  Go To               ${url}
```
