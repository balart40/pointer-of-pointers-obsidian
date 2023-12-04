---
tags:
  - Kubernetes
  - docker
  - containers
---
## Understanding Deployments

- The **deployment** is the standard for running applications in Kubernetes
- It offers features that add to the scalability and reliability of the application
	- **Scalability:** scaling the number of application instances
	- **Updates and Update strategy:** zero-downtime application updates
- It protects Pods and will automatically restart them if anything goes wrong
- Use kubectl **create deploy** to create deployments

The deployments include configurations such as labels to identify the Pods that belong to the Deployment.  See the example of the kubernetes dashboard below

```
kubectl describe deployments.apps kubernetes-dashboard -n kubernetes-dashboard
```

```
Name:                   kubernetes-dashboard
Namespace:              kubernetes-dashboard
CreationTimestamp:      Tue, 24 Oct 2023 16:44:45 -0700
Labels:                 addonmanager.kubernetes.io/mode=Reconcile
                        k8s-app=kubernetes-dashboard
                        kubernetes.io/minikube-addons=dashboard
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               k8s-app=kubernetes-dashboard
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:           gcp-auth-skip-secret=true
                    k8s-app=kubernetes-dashboard
  Service Account:  kubernetes-dashboard
  Containers:
   kubernetes-dashboard:
    Image:      docker.io/kubernetesui/dashboard:v2.7.0@sha256:2e500d29e9d5f4a086b908eb8dfe7ecac57d2ab09d65b24f588b1d449841ef93
    Port:       9090/TCP
    Host Port:  0/TCP
    Args:
      --namespace=kubernetes-dashboard
      --enable-skip-login
      --disable-settings-authorizer
    Liveness:     http-get http://:9090/ delay=30s timeout=30s period=10s #success=1 #failure=3
    Environment:  <none>
    Mounts:
      /tmp from tmp-volume (rw)
  Volumes:
   tmp-volume:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   kubernet
```

## Understanding Deployment Scalability

- To manage scalability, the Deployment creates a ReplicaSet
- Do NOT manage ReplicaSets directly, manage through the Deployment only

| Command | Description |
| :----------------  | :----: |
| kubectl create deploy deployment-Name --image=Image-Name --replicas=N | Create a new deployment with the specified image and number of replicas|
| kubectl describe deployment DeploymentName | Detailed information about a specific deployment | 
| kubectl scale deployment DeploymentName --replicas=N| | 
| kubectl edit deployment DeploymentName| Open a text editor to modify the configuration of a specific deployment| 
