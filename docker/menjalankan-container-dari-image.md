### Menjalankan container dari image

Otomatis akan merunning container menggunakan image bernama rasyid-php7 dengan tag 1.0 dan masuk ke shell ash (asumsi di bawah image menggunakan alpine linux), dan memberi nama container sebagai 'test'

```
$ docker run --name test -ti rasyid-php7:1.0 /bin/ash
```

Menjalankan container sebagai daemon

```
$ docker run -d --name test -ti rasyid-php7:1.0 /bin/ash
```

Menjalankan container, masuk ke bash dan otomatis menghapus container jika menjalankan perintah exit

```
$ docker run --rm --name test -ti rasyid-php7 /bin/ash
```
