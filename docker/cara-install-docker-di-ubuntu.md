# Cara Install Docker Engine Di Ubuntu

Asumsi kali ini menggunakan ubuntu Xenial Xerus (16.04)

1. Buka terminal
2. Kita pastikan apt bisa bekerja dengan https, dan ca-certificate telah terinstall

   ```
   $ sudo apt-get install apt-transport-https ca-certificates
   ```

3. Tambahkan GPG key ini

   ```
   $ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
   ```

4. Buka file /etc/apt/sources.list.d/docker.list melalui editor pilihan. Jika file belum ada, buatlah terlebih dahulu.
5. Hapus baris yang telah ada sebelumnya (jika memang docker.list telah ada sebelumnya).
6. Tambahkan entry untuk Ubuntu xenial xerus pada file tersebut

   ```
   deb https://apt.dockerproject.org/repo ubuntu-xenial main
   ```

7. Simpan dan tutup file docker.list
8. Lakukan apt update

   ```
   $ sudo apt-get update
   ```

9. Purge repo lama (jika memang ada)

   ```
   $ sudo apt-get purge lxc-docker
   ```

10. Install docker-engine

   ```
   $ sudo apt-get install docker-engine
   ```

11. Jalankan daemon untuk docker

   ```
   $ sudo service docker start
   ```

12. Verifikasi bahwa docker telah terinstalasi dengan baik dengan menjalankan command ini

   ```
   $ sudo docker run hello-world
   ```

Maksud perintah tersebut adalah, akan menjalankan images dari [docker hub](https://hub.docker.com/) yang bernama hello-world, docker akan otomatis pull images tersebut jika memang belum tersedia di lokal, dan otomatis akan menjalankannya dalam container.
