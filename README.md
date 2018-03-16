This reproduces the problem of trying to lazily proxy to a backend service.

```
$ minikube start
$ eval $(minikube docker-env)
$ kubectl config use-context minikube
$ build -t upstream_and_map:frontend containers/frontend
$ kubectl apply -f k8s/frontend
$ kubectl apply -f k8s/backend
$ minikube service frontend --url
```

Tailing the logs:

```
$ kubectl logs frontend-xyz -f

...
2018/03/16 14:01:25 [error] 7#7: *2 no resolver defined to resolve backend, client: 172.17.0.1, server: , request: "GET / HTTP/1.1", host: "192.168.99.100:32700"
```
