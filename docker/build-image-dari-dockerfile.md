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

  SHELL ["/bin/ash", "-c"]
  RUN apk update
  RUN apk upgrade

  RUN cat /etc/alpine-release

  RUN apk add nginx
  ```

  Info lebih lanjut terkait instruksi yang bisa digunakan pada Dockerfile, bisa merujuk di [dokumentasi dockerfile](https://docs.docker.com/engine/reference/builder/).

4. Jalankan perintah berikut (di dalam direktori tersimpanya Dockerfile) untuk menciptakan image berdasarkan Dockerfile, yang akan kita beri nama/tag rasyid-php7

  ```
  $ rasyid build -t rasyid-php7 .
  ```
