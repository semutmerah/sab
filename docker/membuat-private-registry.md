# Membuat Private Registry

Start registry

```
$ docker run -d -p 5000:5000 --name registry registry:2
```

pull (atau build) image dari hub

```
$ docker pull ubuntu
```

berikan tag pada image tersebut agar pointing ke registry

```
$ docker tag ubuntu localhost:5000/imagesaya
```

push image tersebut ke lokal registry

```
$ docker push localhost:5000/imagesaya
```

pull kembali

```
$ docker pull localhost:5000/imagesaya
```

stop registry dan hapus semua data

```
$ docker stop registry && docker rm -v registry
```
