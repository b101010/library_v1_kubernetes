## Library v1 + kubernetes

- A docker imageket pusholtam dockerhubra
- A meglévő docker-compose.yml filet átalakítottam
- a kompose segítségével konvertáltam

```bash
kubectl apply -f kubemanifests.yaml

service/flask created
service/mysql created
service/nginx created
deployment.apps/flask created
networkpolicy.networking.k8s.io/hw2-my-network configured
deployment.apps/mysql created
deployment.apps/nginx created
```

```bash
kubectl get pods

NAME                     READY   STATUS    RESTARTS   AGE
flask-775c46b646-4kqrx   1/1     Running   0          37s
mysql-565b46b7c4-nfhwl   1/1     Running   0          37s
nginx-5bbf767dd-qnwf4    1/1     Running   0          37s
```

```bash
kubectl get svc

NAME         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
flask        ClusterIP      10.102.126.223   <none>        5000/TCP       62s
kubernetes   ClusterIP      10.96.0.1        <none>        443/TCP        60m
mysql        ClusterIP      10.107.217.35    <none>        3306/TCP       62s
nginx        LoadBalancer   10.103.186.24    <pending>     80:32435/TCP   62s
```

```bash
minikube service nginx --url
http://192.168.49.2:32435
```

```bash
curl http://192.168.49.2:32435/search/author/rowling | json_pp

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   932  100   932    0     0  30917      0 --:--:-- --:--:-- --:--:-- 32137
[
   {
      "created_at" : "Mon, 06 Feb 2023 15:14:34 GMT",
      "flname" : "J.K. Rowling",
      "id" : 6298,
      "lib_date" : "Mon, 04 Jun 2007 00:00:00 GMT",
      "pub_date" : "Mon, 01 Jan 2001 00:00:00 GMT",
      "publisher" : "Arthur A. Levine",
      "title" : "Harry Potter Schoolbooks Box Set: Two Classic Books from the Library of Hogwarts School of Witchcraft and Wizardry",
      "updated_at" : "Mon, 06 Feb 2023 15:14:34 GMT"
   },
   {
      "created_at" : "Mon, 06 Feb 2023 15:14:45 GMT",
      "flname" : "J.K. Rowling",
      "id" : 7703,
      "lib_date" : "Mon, 24 Jan 2011 00:00:00 GMT",
      "pub_date" : "Sat, 16 Jul 2005 00:00:00 GMT",
      "publisher" : "Scholastic Inc.",
      "title" : "Harry Potter and the Half-Blood Prince",
      "updated_at" : "Mon, 06 Feb 2023 15:14:45 GMT"
   },
   {
      "created_at" : "Mon, 06 Feb 2023 15:14:49 GMT",
      "flname" : "J.K. Rowling",
      "id" : 8120,
      "lib_date" : "Tue, 31 Jan 2012 00:00:00 GMT",
      "pub_date" : "Sat, 01 Jan 2005 00:00:00 GMT",
      "publisher" : "Scholastic",
      "title" : "Harry Potter Collection",
      "updated_at" : "Mon, 06 Feb 2023 15:14:49 GMT"
   }
]

```