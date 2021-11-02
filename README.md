# Homework api gateway

## Preinstall
If you are using minikube, turn on ingress addon with command
```bash
minikube addons  enable ingress
```

## Installation nginx ingress
Add repo
```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```
Install nginx-ingress
```bash
helm install --version "3.35.0" -n nginx-ingress -f ./hw-apigtw-helm/nginx-ingress/nginx.yaml \
ingress-nginx ingress-nginx/ingress-nginx
```

Apply routes
```bash
kubectl apply -f ./hw-apigtw-helm/nginx-ingress/routes.yaml

minikube service -n nginx-ingress ingress-nginx-controller
```

## Install auth service

namespace default
```bash
helm install gateway ./hw-apigtw-helm/gateway
```

## Install application

namespace default
```bash
helm install myapplication ./hw-apigtw-helm/app
```

## Uninstall

```bash
helm un myapplciation
helm un gateway
```


## Api
Install newman if you wish:
```
brew install newman
```
and run prepared test
```
newman run ./homework-apigateway.postman_collection.json
```
or import this file to postman, and start manually

Link to course: https://otus.ru/lessons/microservice-architecture