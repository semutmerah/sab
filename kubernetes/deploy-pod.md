# Deploy Pod

Let say, kita punya file konfigurasi bernama deployment.yaml :

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

Lalu kita juga sudah terkoneksi ke kubernetes server atau minikube server dengan kubectl.
Maka, step untuk deploy service tomcat di atas adalah:

1. Buka terminal, dan masuk ke direktori root dimana file deployment.yaml di atas berada
2. Jalankan perintah ```$ kubectl apply -f ./deployment.yaml```
3. Proses perintah di atas mungkin akan lama, terutama jika image container berada di remote location

Untuk mengecek status proses deploy pods, bisa dilakukan dengan:
1. Jalankan perintah ```$ kubectl get pods```. Outputnya kira-kira seperti ini:

```
$ kubectl get pods
NAME                                 READY   STATUS    RESTARTS   AGE
tomcat-deployment-56ff5c79c5-z5wks   1/1     Running   0          5m
```

2. Jalankan perintah ```$ kubectl describe pods tomcat-deployment-56ff5c79c5-z5wks```, di mana ```tomcat-deployment-*``` diambil dari hasil output perintah ```$ kubectl get pods``` sebelumnya