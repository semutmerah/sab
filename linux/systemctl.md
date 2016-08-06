### Apa itu systemctl?

systemctl adalah perintah yang digunakan untuk mengatur systemd (daemon) services yang saat ini menjadi standar pada linux. Sistem operasi ubuntu telah menerapkan ini semenjak versi 15.04.

Perintah-perintah di bawah diasumsikan dijalankan pada sistem operasi ubuntu 15.04 ke atas.

### Menjalankan dan menghentikan services

```
$ sudo systemctl start application.service
```

Atau, kita bisa menyederhanakannya dengan menghilangkan .service (karena systemd sudah tau kemana harus mencarinya)

```
$ sudo systemctl start application
```

Untuk menghentikan service, kita bisa menggunakan perintah stop:

```
$ sudo systemctl stop application.service
```

### Restart dan reload services

```
$ sudo systemctl restart application.service
```

```
$ sudo systemctl reload application.service
```

### Enabling dan disabling service

Dengan menjalankan ini, kita bisa mengatur apakah suatu service ingin dijalankan ketika mesin boot atau tidak

```
$ sudo systemctl enable application.service
```

```
$ sudo systemctl disable application.service
```

### Melihat status dari sebuah service

```
$ systemctl status application.service
```

### Listing units yang sedang aktif

```
$ systemctl list-units
```

Jika ingin me-list semua units baik statusnya aktif atau tidak, bisa menambahkan flag --all di akhir perintah:

```
$ systemctl list-units --all
```

Bisa juga melakukan filter dengan flag --type, misalnya jika kita ingin menampilan unit yang tipenya service:

```
$ systemctl list-units --type=service
```

### Menampilkan unit file

```
$ systemctl cat application.service
```

### Mengedit unit file

Misal kita ingin melakukan konfigurasi pada unit file service nginx

```
$ sudo systemctl edit nginx.service
```

Perintah ini akan membuat sebuah file kosong/snippet yang bisa kita gunakan untuk meng-override unit tersebut. Cara ini lebih baik karena kita tidak perlu menulis ulang semua konfigurasi dari unit, cukup menulis baris/direktif yang memang ingin kita ubah. File ini biasanya akan terletak di /etc/systemd/system. Pada contoh ini kita mengedit nginx service, maka direktori akan tercipta di /etc/systemd/system/nginx.service.d/

Jika memang menginginkan untuk mengedit file unit secara keseluruhan, perintahnya adalah:

```
$ sudo systemctl edit --full nginx.service
```

Untuk perintah ini, file unit yang telah diubah akan disimpan di /etc/systemd/system

### Menghapus custom/overrided unit file

Untuk menghilangkan unit file yang telah dimodifikasi, cukup menjalankan perintah:

```
$ sudo rm -r /etc/systemd/system/application.service.d
```

Atau jika full unit:

```
$ sudo rm /etc/systemd/system/application.service
```

Setelah menghapus, jangan lupa reload kembali dengan perintah:

```
$ sudo systemctl daemon-reload
```
