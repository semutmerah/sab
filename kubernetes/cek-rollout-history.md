# Cek Rollout History

Use case:

- Kita punya deployment bernama ```tomcat-deployment```, yang telah melakukan beberapa kali revisi

Maka untuk melihat history rollout nya, bisa dengan menjalankan perintah:

```
$ kubectl rollout history deployment/tomcat-deployment

Contoh output:
deployment.extensions/tomcat-deployment 
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

Untuk melihat detil revision tertentu, bisa dengan menjalankan perintah:

```
$ kubectl rollout history deployment/tomcat-deployment --revision=2

Contoh output:
deployment.extensions/tomcat-deployment with revision #2
Pod Template:
  Labels:	app=tomcat
	pod-template-hash=138885474
  Containers:
   tomcat:
    Image:	tomcat:9.0.1
    Port:	8080/TCP
    Host Port:	0/TCP
    Environment:	<none>
    Mounts:	<none>
  Volumes:	<none>
```
