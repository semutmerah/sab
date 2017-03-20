## Lock dan Unlock bootloader

Pada kasus dimana kita ingin menginstall custom recovery atau custom ROM, maka diperlukan untuk mengunlock bootloader.
Jalankan perintah ini dengan kondisi sudah masuk di bootloader. Asumsi perintah ini dijalankan pada ubuntu.

Unlock bootloader:
```
$ sudo $(which fastboot) oem unlock
```

Lock bootloader:
```
$ sudo $(which fastboot) oem lock
```
