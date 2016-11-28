## Mendapatkan UDID iPhone dari terminal

```
$ lsusb -s :`lsusb | grep iPhone | cut -d ' ' -f 4 | sed 's/://'` -v | grep iSerial | awk '{print $3}'
```
