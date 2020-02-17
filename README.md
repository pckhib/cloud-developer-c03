[![Build Status](https://travis-ci.com/pckhib/udacity-cloud-developer-c3.svg?branch=master)](https://travis-ci.com/pckhib/udacity-cloud-developer-c3)

# Udacity Cloud Developer - Course 03

## Refactor Udagram App into Microservices and Deploy

- [Docker](#Docker)
- [Kubernetes](#Kubernetes)


## Docker

### Prerequisites

- **Docker** - [Get Started](https://www.docker.com/get-started)

### Deploy
The application can be started on a local system using Docker Compose.
```shell
$ docker-compose -f udacity-c3-deployment/docker/docker-compose.yaml up
```


## Kubernetes

### Prerequisites

- **Docker** - [Get Started](https://www.docker.com/get-started)
- **kubectl** - [Installation](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- **kops** - [Installation](https://github.com/kubernetes/kops#installing) and [AWS Quick-Start](https://github.com/kubernetes/kops/blob/master/docs/getting_started/aws.md)
