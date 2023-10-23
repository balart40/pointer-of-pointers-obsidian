---
tags:
  - Kubernetes
  - containers
---
### KCNA
- Kubernetes and Cloud Native Associate
### CKAD
- Certified Kubernetes App Developer
### CKA
- Certified Kubernetes Administrator
### CKS
- Certified Kubernetes Security
### What is a container?
- A self-container ready-to-run app
- Have all on board that is required to start the app
- To start  one, you require a container runtime
### What is a container run time?
- Container runtime is running on a host platform and and establishes communication between the local host kernel and the container

|-----------------|
|:-:|
|App Libraries gLibc |
|Runtime |
|Kernel |

**Images**
- Are read-only environments that contain the runtime environment, including app and its required libraries

**Containers**
- Are the isolated runtime environment where the app is running. By using namespaces, the containers can be offered as a strictly isolated environments.

**Registries**
- Are used to store  images. Docker Hub is a common registry
- Another is quay.io

**Containers**
- Containers are linux
- Use linux kernel namespaces for isolation
- Network
- file
- Users 
- Processes 
- IPCs

Linux CGroups - resolve allocation and limitation

**Container Run time**

- The container runtime allows for starting and running the container on top of the host OS
- The container runtime is responsible for all parts of running the container which are not already 