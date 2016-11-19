### Mounting volume

Konsep docker adalah portability. Oleh karena itu, cara terbaik untuk mounting volume adalah ketika menjalankan image. Contoh perintahnya:

```
$ docker run -d -v /home/username/directory:/var/www/localhost/htdocs -ti rasyid-php7
```

Maksud dari perintah di atas, docker akan me-mounting direktori /home/username/directory pada sisi host, ke directory /var/www/localhost/htdocs pada sisi environment docker.
