#  Node project

The main goal is to build a Docker image of the project and publish it on Docker Hub, so we can use it to create a kubernetes deployment that we will expose using minikube tunnel.
The application crash if we hit **/error** endpoint
# Steps

## Clone repo
```console
git clone <repo-url>
```

## Build image
```console
docker build -t <dockerID>/node-app:1.0.0 .
```

## Publish image on Docker Hub

```console
docker push <dockerID>/node-app:1.0.0
```

## Create deployement

```console
kubectl create deployment node-deployment --image <dockerID>/node-app:1.0.0
```

## Create service

```console
kubectl expose deployment/node-deployment --type LoadBalancer --port 8080
```

## Expose Service with minikube

```console
minikube service node-deployment
```

## Scale the application

```console
kubectl scale deployment/node-deployment --replicas 5
```