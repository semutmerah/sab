# Set Secrets

Secret adalah metode di kubernetes untuk menyimpan informasi yang sensitif seperti password, oauth tokens, dan ssh keys.

Untuk membuat secret, ada 2 cara:

1. Dari file
2. Dari command (literal)

### 1. Dari file

Misal, kita punya file yang sudah berisi informasi tentang username dan password:

```
# Create files needed for rest of example.
$ echo -n 'admin' > ./username.txt
$ echo -n '1f2d1e2e67df' > ./password.txt
```

Untuk menyimpannya menjadi secret di kubernetes, maka cukup dengan menjalankan perintah:

```
$ kubectl create secret generic db-user-pass --from-file=./username.txt --from-file=./password.txt
```

### 2. Dari command (literal)

Misal, kita hendak menyimpan secret yang akan digunakan sebagai password mysql, maka bisa dilakukan dengan perintah:

```
$ kubectl create secret generic mysql-pass --from-literal=password=PasswordDbNyaIni
```

