# Expose

Expose adalah salah satu perintah di ```kubectl``` yang fungsinya meng-expose service yang ada dalam satu pod sehingga bisa menerima traffic.

Untuk mengerti tentang perintah expose ini, maka perlu memahami apa itu ```Kubernetes Service```, yang secara lengkap pemaparannya bisa dilihat di [artikel ini](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/)

Untuk contoh sederhana, katakan kita punya use case seperti ini:

1. Kita punya satu pod yang telah deploy dan ready bernama ```tomcat-deployment``` , yang di dalamnya terdapat tomcat service. Namun kita belum bisa mengakses tomcat tersebut dari luar cluster, karena kita belum memiliki Kubernetes Service yang mengekspose service di dalam pod tersebut.
2. Kita ingin mengekspose tomcat server tersebut dari luar melalui NodeIP:NodePort

Maka untuk case di atas, yang perlu dilakukan adalah menjalankan perintah:

```
$ kubectl expose deployment tomcat-deployment --type=NodePort
```

Flag ```--type=Node``` sendiri pemaparannya sudah disampaikan pada dokumentasi kubernetes service di atas.

Jika pakai minikube, maka untuk mengetahui alamat lengkap dari service ```tomcat-deployment``` tersebut bisa dilakukan dengan perintah:

```
$ minikube service tomcat-deployment --url
http://192.168.99.100:31163
```

Yang berarti berdasarkan output, kita bisa mengunjungi tomcat server tersebut dari luar dengan mengakses ke ```http://192.168.99.100:31163```