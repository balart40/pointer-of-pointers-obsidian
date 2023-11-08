---
tags:
  - Kubernetes
  - docker
  - containers
---

### Understanding Deployment options

Kubernetes can be deployed in many environments:
- In public cloud (GCP, AWS, Azure, etc.)
- On-premise in a data center
- Using Minikube or other kubernetes distributions
### Minikube

Minikube is an all-in-one Kubernetes solution where both controller and worker functionality are typically offered on a single node, but it can also be configured on multiple nodes.

To use Minikube you should have at least 2 Gb of RAM (4 recommended) and 2 virtual CPUs
### Install Minikube on Mac

Official K8s Site: [Link](https://minikube.sigs.k8s.io/docs/start/)

### Run Minikube

Depending on your driver settings you can either use

`minikube start

or

`minikube start --vm-driver=docker

Then you can check the status with the following command

`minikube status

### Session 4 - Lab

Usually the deployment will consist on a **Controller node** which will govern then **Worker nodes**

From the dashboard once the nginx app has been deployed you can get the deployment info with the following CLI below

`kubectl get deployments

Then you can get the deployment configuration and port it to a yaml file

`kubectl get deployment nging-app -o yaml > nging-app-deployment.yaml

The same approach can be followed for the pods of the deployment

`kubectl get pods

And the get the pod configuration

`kubectl get pod nging-app-54d577c49c-9lsf2 -o yaml > ning-app-pod.yaml


