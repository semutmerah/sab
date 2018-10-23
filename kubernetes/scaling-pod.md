# Scaling Pod

Let say, kita sudah punya satu pod yang berjalan dengan konfigurasi:

```
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: tomcat-deployment
spec:
  selector:
    matchLabels:
      app: tomcat
  replicas: 1
  template:
    metadata:
      labels:
        app: tomcat
    spec:
      containers:
      - name: tomcat
        image: tomcat:9.0
        ports:
        - containerPort: 8080
```

Untuk menaikkan jumlah pod / upscaling, ada 2 cara:
1. Edit file deployment.yaml di atas, pada baris ```replicas``` menjadi 4 misalnya. Lalu deploy ulang menggunakan deployment.yaml yang telah diupdate
2. Jalankan perintah ```$ kubectl scale --replicas=4 deployment/tomcat-deployment```

Perintah no 2 memungkinkan kita untuk mencegah down ketika proses upscaling. 

Selain itu, pada case ini, kita juga perlu mengekspose kembali service dengan flag ```--type=LoadBalancer```, dengan perintah:

```
$ kubectl expose deployment tomcat-deployment --type=LoadBalancer --port=8080 --target-port=8080 --name=tomcat-load-balancer
```