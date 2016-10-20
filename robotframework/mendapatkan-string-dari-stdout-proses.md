# Mendapatkan string dari stdout proses


```
*** Settings ***
Documentation     A resource for global
Library           Process


*** Keywords ***
Get String From Process
  Run Process       adb -s ${udid} shell pm list packages | grep ${package_name}      shell=True    alias=proc
  ${result}         Get Process Result              proc      stdout=true
  Log               ${result}
```
