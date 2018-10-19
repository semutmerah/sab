# Linking Container

Dengan linking container, kita bisa membuat dua atau lebih container saling berkomunikasi.
Asumsi, kita punya use case aplikasi web python yang terintegrasi dengan redis server. Maka step untuk mengaktifkan linking container adalah sebagai berikut:

1. run redis container dengan perintah ```$ docker build -d --name redis redis:3.2.0```
2. run python container yang telah terintegrasi dengan web app, dan hubungkan dengan redis container dengan perintah ```$ docker run -d -p 5000:5000 --link redis pythonapp```

Bagaimana linking container ini bekerja? Jawabannya adalah ketika kita menambahkan flag ```--link``` pada perintah ```docker run```, maka docker akan menambahkan hostname container yang kita link di container recipient pada ```/etc/hosts/```, dalam use case di atas recipient nya adalah container ```pythonapp```

Contoh ```/etc/hosts``` recipient yang telah linking dengan container lain adalah seperti ini:

```
127.0.0.1	localhost
::1	localhost ip6-localhost ip6-loopback
fe00::0	ip6-localnet
ff00::0	ip6-mcastprefix
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
172.17.0.2	redis b67e2cb74c30
172.17.0.3	73fe07838d9a
```

Di mana baris ke 2 sebelum line terakhir adalah hasil menambahkan flag ```--link```