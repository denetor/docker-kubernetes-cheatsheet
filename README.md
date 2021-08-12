## Docker
```
sudo service docker start
sudo service docker stop
docker version
docker images
docker run -d --name postgres-test -v ~/docker/postgres/data/test:/var/lib/postgresql/data -e POSTGRES_PASSWORD=easypassword -p 5432:5432 postgres
docker run --name adminer --link postgres-test:db -p 8080:8080 adminer
docker ps
docker exec -ti baa7e0faa296 bash
docker stop baa7e0faa296
docker rm baa7e0faa296
```

### List all networks a container belongs to
```
docker inspect -f '{{range $key, $value := .NetworkSettings.Networks}}{{$key}} {{end}}' [container]
```

### List all containers belonging to a network by name
```
docker network inspect -f '{{range .Containers}}{{.Name}} {{end}}' [network]
```

### Attach a running container to a network
```
docker network connect [network] [container]
```

### With containerA already running, test if containerA can connect to containerB by using its name
```
docker exec [containerA] ping [containerB] -c2
```

## docker-compose
```
docker-compose version
docker-compose up -d
```

## kubernetes/minikube
```
minikube start
minikube dashboard
minikube stop
minikube tunnel

sudo snap install kubectl
kubectl version
kubectl get po -A
kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
kubectl expose deployment hello-minikube --type=NodePort --port=8080
kubectl get services hello-minikube
kubectl port-forward service/hello-minikube 7080:8080
kubectl create deployment balanced --image=k8s.gcr.io/echoserver:1.4
kubectl expose deployment balanced --type=LoadBalancer --port=8080
kubectl get services balanced
minikube delete --all

microk8s status
sudo microk8s get nodes
microk8s kubectl get nodes
microk8s kubectl get services
sudo microk8s status --wait-ready
sudo microk8s enable dashboard dns registry istio
sudo microk8s kubectl get all --all-namespaces
sudo microk8s dashboard-proxy

docker save demonginx > demonginx.tar
sudo microk8s ctr image import demonginx.tar
```
