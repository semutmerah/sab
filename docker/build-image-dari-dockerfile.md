### Build image dari dockerfile

1. Buat direktori untuk menyimpan dockerfile

  ```
  $ mkdir ~/Workspace/docker/php7
  $ cd ~/Workspace/docker/php7
  ```

2. Buat file bernama dockerfile di direktori tersebut

  ```
  $ touch Dockerfile
  ```

3. Edit Dockerfile tersebut dengan editor kesukaan anda

  ```
  $ nano Dockerfile
  ```

  Contoh isi dari dockerfile

  ```
  FROM alpine:edge

  MAINTAINER Rasyid Fahroni <rasyid@rasyidfahroni.com>

  LABEL "contains"="nginx, php7"

  ENV HTDOCS /var/www/localhost/htdocs
  ENV NGINX /etc/nginx
  ENV PHP7 /etc/php7

  RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories;\
  apk update;\
  apk upgrade;\
  apk --no-cache add openrc libseccomp nginx nano php7-fpm php7-curl php7-gd php7-mysqli php7-session php7-zlib php7-opcache

  EXPOSE 80
  ```

  Info lebih lanjut terkait instruksi yang bisa digunakan pada Dockerfile, bisa merujuk di [dokumentasi dockerfile](https://docs.docker.com/engine/reference/builder/).

4. Jalankan perintah berikut (di dalam direktori tersimpannya Dockerfile) untuk menciptakan image berdasarkan Dockerfile, yang akan kita beri repository/tag rasyid-php7:latest. Secara otomatis docker akan membuat tag latest jika tidak kita tambahkan parameter tersebut saat menjalankan perintah, seperti perintah di bawah:

  ```
  $ rasyid build -t rasyid-php7 .
  ```

  Jika ingin menambahkan tag, misal 1.0 (version), maka perintahnya menjadi:

  ```
  $ rasyid build -t rasyid-php7:1.0 .
  ```
