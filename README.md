#  Node project

The main goal is to build a Docker image of the project and publish it on Docker Hub, so we can use it to create a kubernetes deployment that we will expose using minikube tunnel.
The application crash if we hit **/error** endpoint
# Steps

## Clone repo
To clone the repository, you can use the following command followed by the URL of the repository.

```console
git clone <repo-url>
```

## Build image
To build the Docker image, you can use the following command, make sure that you are in the directory containing the Dockerfile.

```console
docker build -t <dockerID>/node-app:1.0.0 .
```

## Publish image on Docker Hub
Before publishing the Docker image, make sure to create repository on Docker Hub first. Tag the image with the repository name and version. And log in to Docker Hub from comman line using the `docker login` command, then you can push your Docker image.

```console
docker push <dockerID>/node-app:1.0.0
```

## Create deployement
To create a Kubernetes deployment from an image use the following command. With `--replicas` option you can specify number of replicas you want to create, otherwise it will create one replica by default.
Make sure that you're using the right kubernetes context.

```console
kubectl create deployment node-deployment --image <dockerID>/node-app:1.0.0 --replicas 5
```

## Create service
To create a service of type LoadBalaner that exposes port 8080 use the following command:

```console
kubectl expose deployment/node-deployment --type LoadBalancer --port 8080
```

## Expose Service with minikube
To expose the kubernetes service use the following command. It will create a new service of type LoadBalancer that exposes the specified service and opens the service URL in a web browser. Minikube uses a tunnel to expose the service to your local machine.

```console
minikube service node-deployment
```
