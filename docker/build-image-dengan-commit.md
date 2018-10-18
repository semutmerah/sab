# Build Image Dengan Commit

Selain dengan menggunakan Dockerfile untuk membuat sebuah docker image, kita juga dapat membuat sebuah docker image dengan menggunakan perintah ```docker commit```.

Yang membedakan adalah, ```docker commit``` ini akan menciptakan image berdasarkan kondisi terakhir dari sebuah docker instance. Contoh penerapannya dalam kondisi real adalah seperti ini:

Use case : Membuat docker image berbasis ubuntu yang sudah terdapat editor nano

1. Pull ubuntu image dari docker hub dengan perintah ```$ docker pull ubuntu:latest```
2. Jalankan ubuntu image ke container bernama ```test```, dan langsung masuk ke bash shell dengan perintah ```$ docker run --name test -ti ubuntu:latest /bin/bash```
3. Di dalam container, jalankan perintah untuk menginstall nano ```apt-get update && apt-get install -y nano```
4. Exit container
5. Buat image dari kondisi terakhir container ```test``` dengan perintah ```$ docker commit test ubuntu/nano```

Image akan tersimpan di repository lokal.