# Resize Swap Pada Partisi LVM

### Ubuntu / Debian
1. Mencari tahu nama dari volume logical swap menggunakan perintah lvs:
```
    $ lvs
    LV VG Attr LSize Origin Snap% Move Log Copy%
    root_lv volgroup0 -wi-ao 7.00G
    swap_lv1 volgroup0 -wi-ao 30.00G
    tmp_lv volgroup0 -wi-ao 3.00G
    usr_lv volgroup0 -wi-ao 7.00G
    var_lv volgroup0 -wi-ao 4.00G
```
2. Matikan partisi swap
```
    $ swapoff /dev/volgroup0/swap_lv1
```
3. Resize partisi swap tersebut, pada contoh ini kita akan menambah size nya 10G
```
    $ lvresize -L+10G /dev/volgroup0/swap_lv1
```
4. Format swap yang telah di resize agar bisa digunakan dengan perintah mkswap
```
    $ mkswap /dev/volgroup0/swap_lv1
```
5. Aktifkan kembali volume swap
```
    $ swapon /dev/volgroup0/swap_lv1
```
6. Cek bahwa swap telah berubah dengan perintah di bawah ini
```
    $ free -tom| grep -i swap
```
