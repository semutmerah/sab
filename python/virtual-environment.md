### Virtual Environment

Untuk membuat virtual environment, bisa dengan menggunakan virtualenv

Install dengan menggunakan perintah:

```
$ pip install virtualenv
```

Masuk ke direktori project, dan buat virtual environment:

```
$ cd my_project_folder
$ virtualenv venv
```

Kita juga bisa menentukan interpreter version yang kita inginkan:

```
$ virtualenv -p /usr/bin/python3 venv
```

Untuk memulai menggunakan virtual environment, jalankan perintah ini:

```
$ source venv/bin/activate
```

Jika sudah selesai, untuk keluar dari virtual environment, jalankan perintah ini:

```
$ deactivate
```
