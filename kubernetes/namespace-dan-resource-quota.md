# Namespace dan Resource Quota

Dengan namespace dan resource quota, kita bisa mengklasifikasikan beberapa kubernetes objek dan mengalokasikan resource berdasarkan namespace. Untuk lebih mudah memahaminya, kita bisa gunakan use case ini:


Kita punya deployment yang berisikan tomcat service. Deployment ini akan dijalankan di dalam cluster yang di dalamnya juga sudah berjalan deployment service yang lain. Untuk lebih memudahkan, kita akan menerapkan ```namespace``` untuk kubernetes objek yang terkait tomcat service ini (berupa deployment dan resourcequota). Kita akan berikan namespace bernama ```cpu-limited-tomcat```, dan kita akan menerapkan ```resourcequota``` untuk namespace ini yang akan melimitasi penggunaan cpu hanya sebanyak ```750m``` (yang jika diterjemahkan berarti 75% dari cpu yang dimiliki oleh cluster)

Untuk mencapai hal tersebut, maka yang bisa kita lakukan adalah:

1. Membuat namespace ```cpu-limited-tomcat``` dengan perintah ```$ kubectl create namespace cpu-limited-tomcat```. Atau bisa juga dengan meng-apply / create dari file yaml yang berisikan:

```
apiVersion: v1
kind: Namespace
metadata:
  name: cpu-limited-tomcat
spec:
  finalizers:
  - kubernetes
```

2. Membuat ```resourcequota``` yang melimitasi cpu menjadi 750m berdasarkan file yaml ini (note namespace yang kita set di metadata):

```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-resources
  namespace: cpu-limited-tomcat
spec:
  hard:
    limits.cpu: "750m"
```

3. Membuat deployment ```tomcat-deployment``` berdasarkan yaml ini (note namespace, replicaset, serta cpu yang di set di sini):

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tomcat-deployment
  namespace: cpu-limited-tomcat
spec:
  selector:
    matchLabels:
      app: tomcat
  replicas: 3
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
        resources:
          requests:
            cpu: "251m"
          limits:
            cpu: "251m"
```

Jika ketiga step di atas sudah dilakukan, mari kita coba cek status ```tomcat-deployment``` dengan menjalankan perintah ```$ kubectl describe deployment tomcat-deployment```. Perhatikan outputnya:

```
Name:                   tomcat-deployment
Namespace:              cpu-limited-tomcat
CreationTimestamp:      Wed, 31 Oct 2018 21:16:09 +0700
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 1
                        kubectl.kubernetes.io/last-applied-configuration:
                          {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"name":"tomcat-deployment","namespace":"cpu-limited-tomcat"},"spe...
Selector:               app=tomcat
Replicas:               3 desired | 2 updated | 2 total | 2 available | 1 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=tomcat
  Containers:
   tomcat:
    Image:      tomcat:9.0
    Port:       8080/TCP
    Host Port:  0/TCP
    Limits:
      cpu:  251m
    Requests:
      cpu:        251m
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type             Status  Reason
  ----             ------  ------
  Available        False   MinimumReplicasUnavailable
  ReplicaFailure   True    FailedCreate
  Progressing      False   ProgressDeadlineExceeded
OldReplicaSets:    <none>
NewReplicaSet:     tomcat-deployment-c98d4c976 (2/3 replicas created)
Events:            <none>
```

Pada bagian ```Replicas```, kita bisa lihat bahwasanya hanya terbentuk 2 replica dari 3 replica yang kita minta. Pada ```Conditions``` di type ```Progressing``` pun bisa kita lihat gagal dengan alasan ```ProgressDeadlineExceeded```. Ini karena kita telah melewati batasan resourcequota yang telah ditetapkan yaitu sebesar 750m. Sedangkan, pada deployment kita mengeset bahwa cpu limit adalah 251m, dimana 251 * 3 = 753, sehingga satu replica / pod tidak akan bisa dijalankan.