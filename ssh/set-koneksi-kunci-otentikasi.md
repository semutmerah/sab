# Set Koneksi Menggunakan Kunci Otentikasi

#### Generate key di sisi client

Jalankan perintah di bawah ini:

```
$ ssh-keygen -t rsa
```

Secara default, key akan tersimpan di ~/.ssh/id_rsa (sistem akan generate id_rsa dan id_rsa.pub, file dengan akhiran pub adalah public key, sedangkan satunya adalah private key), bisa diubah jika diinginkan

Jika ingin sekuriti yang lebih baik, maka bisa menggunakan 4096 bit dengan perintah di bawah ini:

```
$ ssh-keygen -t rsa -b 4096
```

#### Copy public key ke server (cara mudah)

Jalankan perintah di bawah ini:

```
$ ssh-copy-id username@remote-host
```

Asumsi jika username server adalah 'joko' dan ip server adalah 10.10.10.1, maka perintahnya adalah:

```
$ ssh-copy-id joko@10.10.10.1
```

Yang dilakukan oleh perintah ini adalah, akan meng-copy seluruh public key yang ada di client pada direktori ~/.ssh/ ke server pada file ~/.ssh/authorized_keys

Anda mungkin akan melihat pesan seperti di bawah ini ketika menjalankan perintah tersebut:

```
The authenticity of host '10.10.10.1 (10.10.10.1)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
```

Ini hanya pemberitahuan jika komputer anda belum pernah mengenali remote-host/server. Ketik yes lalu enter untuk melanjutkan.

Pada beberapa OS, mungkin anda tidak dapat menjalankan perintah ssh-copy-id, maka alternatifnya adalah dengan perintah di bawah ini:

```
$ cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

#### Copy public key ke server (cara manual)

Pada beberapa kesempatan, mungkin hanya dengan cara manual anda bisa menambahkan public key ke server/remote-host.

Untuk copy dengan cara manual, pertama jalankan perintah ini untuk melihat isi dari public key yang telah di generate sebelumnya, pada kali ini asumsi public key nya adalah id_rsa.pub :

```
cat ~/.ssh/id_rsa.pub
```

Anda akan melihat konten key tersebut, yang kira-kira terlihat seperti ini :

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCqql6MzstZYh1TmWWv11q5O3pISj2ZFl9HgH1JLknLLx44+tXfJ7mIrKNxOOwxIxvcBF8PXSYvobFYEZjGIVCEAjrUzLiIxbyCoxVyle7Q+bqgZ8SeeM8wzytsY+dVGcBxF6N4JS+zVk5eMcV385gG3Y6ON3EG112n6d+SMXY0OEBIcO6x+PnUSGHrSgpBgX7Ks1r7xqFa7heJLLt2wWwkARptX7udSq05paBhcpB0pHtA1Rfz3K2B+ZVIpSDfki9UVKzT8JUmwW6NNzSgxUfQHGwnW7kj4jp4AT0VZk3ADw497M2G/12N0PPB5CnhHf7ovgy6nL1ikrygTKRFmNZISvAcywB9GVqNAVE+ZHDSCuURNsAInVzgYo9xgJDW8wUw2o8U77+xiFxgI5QSZX3Iq7YLMgeksaO4rBJEa54k8m5wEiEE1nUhLuJ0X/vh2xPff6SQ1BL/zkOhvJCACK6Vb15mDOeCSq54Cr7kvS46itMosi/uS66+PujOO+xt/2FWYepz6ZlN70bRly57Q06J+ZJoc9FfBCbCyYH7U/ASsmY095ywPsBo1XQ9PqhnN1/YOorJ068foQDNVpm146mUpILVxmq41Cj55YKHEazXGsdBIbXWhcrRf4G2fJLRcGUr9q8/lERo9oxRm5JFX6TCmj6kmiFqv+Ow9gI0x8GvaQ== demo@test
```

Copy semua isi pada file tersebut, lalu pastekan pada sisi remote-host/server pada file ~/.ssh/authorized_keys menggunakan editor kesukaan anda. Jika sebelumnya sudah ada isi pada file tersebut, cukup tambahkan pada baris paling bawah.


#### Set remote-host untuk me-nonaktifkan otentikasi password

Hal terakhir yang perlu kita setting adalah mematikan konfigurasi pada ssh di remote host agar tidak menerima password sebagai salah satu otentikasi.

Buka file ini menggunakan editor kesukaan anda :

```
$ nano /etc/ssh/sshd_config
```

Di dalam file tersebut, cari sebuah baris yang berisi 'PasswordAuthentication'. Baris ini mungkin diberikan tanda komentar '#', hapus tanda komentar tersebut dan set nilainya menjadi 'no':

```
PasswordAuthentication no
```

Simpan ubahan, dan restart service ssh

```
/etc/init.d/ssh restart
```

Sekarang coba kembali login dari klient ke remote host, seharusnya sistem tidak akan meminta memasukkan password.
