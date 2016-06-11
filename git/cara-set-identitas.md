# Cara Set Identitas

Asumsi di sini adalah menggunakan linux dengan bash shell

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@contoh.com
```

Dengan command di atas, maka git akan mengeset konfigurasi tersebut secara global, jika ingin mengeset hanya pada repo tertentu, maka cukup jalankan command tersebut di dalam direktori repo, dan hilangkan parameter --global, contoh nya:

```
$ git config user.name "John Doe"
$ git config user.email johndoe@contoh.com
```
