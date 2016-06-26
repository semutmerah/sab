# Hapus Semua Package (Ubuntu)

Jalankan salah satu dari 2 command di bawah ini:

```
$ pip list | awk '{print $1}' | sudo -H xargs pip uninstall -y
```

atau

```
$ pip freeze | sudo -H xargs pip uninstall -y
```
