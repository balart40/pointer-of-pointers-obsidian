---
tags:
  - Kubernetes
  - docker
  - Pod
---
## What is a Pod

- It's an abstraction of a server
- It also can run multiple containers within a single Namespace

The **Pod** is the minimal entity that can be managed by Kubernetes

**Kubernetes does not manage containers directly, it manages them through Pods**

- From a container's perspective a Pod is an entity that runs typically one or more containers by using container images
- Typically **Pods** are only started through a **deployment** because "naked" Pods are not rescheduled in case of a node failure

Naked Pods disadvantages
- Zero downtime when update
- Not re-scheduled in case of failure
- Cannot scale 
- cannot be replaced automatically

Pods are managed through `kubectl` CLI command

Below we show three commonly used `kubectl`commands 

| Command               | Description |
| :----------------  | :----: |
| `kubectl run mynginx --image=nginx`     | Create run a Pod called "mynginx" using a default image |
| `kubectl get pods `| List the Pods running in the cluster in the default namespace| 
| `kubectl get pods -o yaml`| Provides insight on all Pod parameters| 
| `kubectl describe pods`| Show all details about a pod including information about containers running within|

## YAML

- YAML is a human readable data serialization language
- It is perfect for DevOps to create input files to manage objects into different systems like Kubernetes and Ansible
- It uses indentation to identify relations
- When combined with Github, its an excellent way to manage and update configuration in a structured way

kubectl CLI commands uses the **imperative way** whilst 

YAML files uses the **declarative way**

All of the YAML manifest ingredients are defined in the API
- **api version**
- **kind**
- **metadata:** Administrative information about the object
- **spec**

Use the kubectl explain to get more information about the basic properties

The container spec, the following parts are needed 
- **Name:** name of the container
- **image:** The container image that should be used
- **command:** The command the container should run
- **args:** arguments that are used by the command
- **env:** environment variables that should be used by the container

These are part of the pod.spec.container.spec which can be checked with `kubectl explain`

To generate YAML files we can first use the `dry-run` argument which simulates the command and using `client`to specify the simulation from the client side. The full command to generate a YAML file would look like this:

`--dry-run=client -o yaml` will generate the file

Use `--dry-run=client -o yaml > my.yaml` as an argument to the `kubectl run` and `kubectl create` commands

For example you if you run 

`kubectl run myginx --image=nginx --dry-run=client -o yaml > myginx.yaml`

Will generate the following YAML file

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: myginx
  name: myginx
spec:
  containers:
  - image: nginx
    name: myginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

The following commands will use the YAML file to manage resources in a declarative way

| Command               | Description |
| :----------------  | :----: |
| kubectl create -f my.yaml | is used to create resources from YAML |
| kubectl apply -f my.yaml| will create a resource if it doesn't exits yet and modify if it already exists and has been created with `kubectl apply` earlier|
| kubectl replace -f yaml| will replace a resource with the new configuration as in the YAML file|
| kubectl delete  -f resource.yaml| Delete kubernetes resources defined in a YAML file, effectively removing them from the cluster|

## Understanding and configuring multi-container Pods

- The one-container Pod is the standard
- Single container Pods are easier to build and maintain 
- In a micro-service, different independently managed Pods are connected by resources that can be provided by Kubernetes

There are some defined cases where you might to run multiple container in a Pod
- **Sidecar container:** A container that enhances the primary application, for instance logging
- **Ambassador container:** A container that represents the primary container to the outside world, such as a proxy.
- **Adapter container:** Used to adopt the traffic or data pattern to match the traffic or data pattern in other applications in the cluster.

**Sidecar container**, etc. are not defined by specific Pod properties; from a Kubernetes API resource, it's just a multi-container Pod

Below a example of a multi-container YAML file

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: mynginx
  name: mynginx
spec:
  volumes:
    - name: shared-data
      emptyDir: {}
  containers:
  - image: nginx
    name: mynginx
    volumeMounts:
      - name: shared-data
        mountPath: /usr/share/nginx/html
  - name: ubuntu-container
    image: ubuntu
    volumeMounts:
    - name: shared-data
      mountPath: /pod-data
    command: ["/bin/sh"]
    args: ["-c", "while true; do date >> /pod-data/index.html; sleep 10; done"]
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

## Init Containers

- Init containers is an additional container in a Pod that competes a task before the "regular" container is started 
- The regular container will only be started once the init container has been started
- if the init container has nor run to completion, the main container is not started

The init container can be added in the Pod spec with the `initContainer` field as shown below

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: mynginx
  name: mynginx
spec:
  volumes:
    - name: shared-data
      emptyDir: {}
  initContainers:
    - name: ubuntu-container
      image: ubuntu
      volumeMounts:
        - name: shared-data
          mountPath: /pod-data
      command: ["/bin/sh"]
      args: ["-c", "date >> /pod-data/index.html"]
  containers:
    - image: nginx
      name: mynginx
      volumeMounts:
        - name: shared-data
          mountPath: /usr/share/nginx/html
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

## Namespaces

- A linux namespace implements kernel-level resource isolation 
- Kubernetes offers namespace resources that provide the same functionality
- Different namespaces can be used to strictly separate between customer resources
- Namespaces are used to apply different security related settings
	- Role-Based Access Control (RBAC)
	- Quota

| Command               | Description |
| :----------------  | :----: |
| kubectl create namespace mynamespace | Create a namespace |
| kubectl ... -n namespace| To work in a specific namespace|
| kubectl get ... -all-namespaces| To see resources in all namespaces|

The namespace will be shown in the metadata of the spec as shown below:

```
apiVersion: v1
kind: Pod
metadata:
  ...
  name: MyNgnix
  namespace: default
spec:
   ...
```

