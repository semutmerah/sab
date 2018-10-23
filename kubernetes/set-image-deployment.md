# Set Image Deployment

Use case:

1. Kita punya 1 atau beberapa pod yang sudah aktif di deployment dengan nama ```tomcat-deployment```, namun belum menggunakan versi ```tomcat``` image yang terbaru.
2. Kita ingin menaikkan versi ```tomcat``` image ke image terbaru

Maka untuk mencapai hal ini, kita bisa menggunakan perintah:

```
$ kubectl set image deployment/tomcat-deployment tomcat=tomcat:9.0.1
```