# Autoscale dengan HPA (Horizontal Pod Autoscaler)

Use case:

- Kita punya deployment bernama ```wordpress``` yang telah berjalan di cluster

Maka untuk mengaktifkan autoscale pada deployment tersebut bisa dilakukan dengan 2 cara:

1. Via command line

```
kubectl autoscale deployment wordpress --cpu-percent=50 --min=1 --max=5
```

2. Via yaml file

```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: wordpress
  namespace: default
spec:
  maxReplicas: 5
  minReplicas: 1
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: wordpress
  targetCPUUtilizationPercentage: 50
```

Konfig HPA di atas akan melakukan autoscaling ketika pod dalam deployment menyentuk cpu percentage 50%, dengan ketentuan minimal replica / pod adalah 1, dan maksimal adalah 5

Untuk mengetes autoscale ini di mesin lokal kita (jika pakai minikube), maka bisa dilakukan dengan menjalankan custom load generator bash script:

- Jalankan 1 pod dari busybox dan langsung masuk ke terminal nya
  
  ```
  kubectl run -i --tty load-generator --image=busybox /bin/sh
  ```

- Jalankan simple sh script berikut:
  
  ```
  while true ; do wget -q -O- http://wordpress.default.svc.cluster.local ; done
  ```

- Lalu monitor hpa dengan perintah:
  
  ```
  watch kubectl get hpa
  ```