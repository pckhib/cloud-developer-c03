[![Build Status](https://travis-ci.com/pckhib/udacity-cloud-developer-c3.svg?branch=master)](https://travis-ci.com/pckhib/udacity-cloud-developer-c3)

# Udacity Cloud Developer - Course 03

## Refactor Udagram App into Microservices and Deploy

- [Docker](#Docker)
- [Kubernetes](#Kubernetes)
- [Travis CI](#Travis-CI)


## Docker

### Prerequisites

- **Docker** - [Get Started](https://www.docker.com/get-started)

### Build images
The images required for the application are deployed to [Docker HUB](https://hub.docker.com/u/pckhib).

Alternatively they can be build locally.
```shell
docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml build --parallel
```

To push the images to Docker HUB run
```shell
docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml push
```

### Run application
The application can be started on a local system using Docker Compose.
```shell
docker-compose -f udacity-c3-deployment/docker/docker-compose.yaml up
```


## Kubernetes
Navigate to the K8s folder:
```shell
cd udacity-c3-deployment/k8s
```

### Prerequisites

- **kubectl** - [Installation](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- **kops** (optional) - [Installation](https://github.com/kubernetes/kops#installing) and [AWS Quick-Start](https://github.com/kubernetes/kops/blob/master/docs/getting_started/aws.md)

To check if your cluster is up an running, run ```kubectl get nodes``` or ```kops validate cluster```.

Once the cluster is set up correctly, start deploying your application.

### Environment
First set the environment variables and credentials to connect to AWS.

Therefore update the values and credentials in the files `aws-secret.yaml`, `env-configmap.yaml` and `env-secret.yaml` and deploy them.

```shell
kubectl apply -f aws-secret.yaml
kubectl apply -f env-configmap.yaml
kubectl apply -f env-secret.yaml
```

### Application
Afterwards configure the services and deployments.

```shell
# Services
kubectl apply -f backend-feed-service.yaml
kubectl apply -f backend-user-service.yaml
kubectl apply -f frontend-service.yaml
kubectl apply -f reverseproxy-service.yaml

# Deployments
kubectl apply -f backend-feed-deployment.yaml
kubectl apply -f backend-user-deployment.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f reverseproxy-deployment.yaml
```

To verify if everything is running correctly run ```kubectl get all``` to get an overview about all services, deployments and pods.

### Access Application
In order to connect to the backend and open the frontend locally, you need to forward the ports of the services.
```shell
# Port 8100 of Frontend
kubectl port-forward service/frontend 8100:8100

# Port 8080 of reverseproxy
kubectl port-forward service/reverseproxy 8080:8080
```

### A/B Deployment
In order to use A/B Deployment of the Backend-Feed service, additionally deploy the backend-feed-b application.
```shell
kubectl apply -f backend-feed-b-service.yaml
kubectl apply -f backend-feed-b-deployment.yaml
```

The nginx config uses `split_clients` in order to distribute the requests to both services. Therefore update the reverseproxy.
```shell
kubectl apply -f reverseproxy-ab-deployment.yaml
```

## Travis CI
Travis CI is being used to continuously build and deploy the application.

The status can be tracked [here](https://travis-ci.com/pckhib/udacity-cloud-developer-c3).