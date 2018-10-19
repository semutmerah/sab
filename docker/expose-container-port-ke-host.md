# Expose Container Port Ke Host

Ketika membuat Dockerfile, kita bisa menyematkan reference ```EXPOSE```

```
EXPOSE port_number
```

Reference ini sifatnya sebagai dokumentasi. Untuk benar-benar mengekspose container port ke host, dapat dilakukan dengan menambahkan flag ```-p``` ketika run container

```
$ docker run -d -p host_port:container_port image_name
```

Dengan mengekspose container port ke host, maka port tersebut bisa diakses dengan localhost dari sisi host. Misal, mengekspose port **80** pada aplikasi web server di container, maka kita bisa mengakses web server tersebut dengan mengetikkan ```localhost``` pada web browser di sisi host.