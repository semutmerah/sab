# Headless Mode pada Chrome Browser di Robot Framework

resources.robot
```
*** Settings ***
Library   SeleniumLibrary   15    run_on_failure=Log Source

*** Variable ***
${HOMEPAGE}     http://semutmerah.us/

*** Keywords ***
Open Headless Chrome
  [Arguments]  ${url}
  ${chrome_options}=  Evaluate  sys.modules['selenium.webdriver'].ChromeOptions()  sys, selenium.webdriver
  Call Method   ${chrome_options}    add_argument    no-sandbox
  Call Method   ${chrome_options}    add_argument    headless
  Call Method   ${chrome_options}    add_argument    disable-gpu
  Create Webdriver  Chrome  chrome_options=${chrome_options}
  Go To  ${url}
```

example_testfile.robot
```
*** Settings ***
Suite Setup             Open Headless Chrome        ${HOMEPAGE}
Suite Teardown          Close Browser
Resource                resources.robot

*** Test Case ***
Verify Homepage Opened
  Wait Until Page Contains Element  class=widget-title
```
