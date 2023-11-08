---
tags:
  - Kubernetes
  - containers
  - docker
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

### **Containers**
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
- Container Solutions
	- docker
	- Ixc
	- runc
	- containerId
- OCI - Open Container Initiative
- File System bundle

Docker started in 2013
- Container image format
- Docker file: Building  container images
- Way to mange container images
- a way to run containers
- a way to manage container instance
- A solution to share container images

- Podman alternative to Docker by Redhat
### **Registries**
- Used to provide access to container images
- Anyone can publish in registries
- Docker hub is the biggest registry
	- other quay.io
- Free
#### Managing Container

- Docker ps  { -a  }
	- Show current running container
- Docker start
	- stat container from a locally storage image
- docker stop
	- stop a container using Linux SIGTERM
- docker restart
	- restart currently running container
- Docker kill
	- stop a container using Linux SIGKILL
- Docker rm
	- remove all container files from host OS
- Docker ps
- docker inspect < ID > less
- docker inspect --format='{{NetworkSetting.IPAddress}}' container name

#### Managing Images
- docker images
- docker images ls