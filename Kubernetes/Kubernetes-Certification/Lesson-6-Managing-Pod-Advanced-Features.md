---
tags:
  - docker
  - Kubernetes
  - Pod
---
## Exploring Pod state with kubectl describe

You can use `kubectl describe` to describe Pods state, parameters that are set by default as well as their current settings.

- When deploying a Pod, may parameters are set to a default value
- Use `kubectl describe pod podname-xxx` to see all these parameters and their current setting as they currently are in the etcd
- Use the documentation at [http://kubernetes.io/docs](http://kubernetes.io/docs) for more information about these settings.
## Connecting to a Pod for further inspection

In order to connect to the pod you can use the command `kubectl get pods` as shown in the example below

```
$ kubectl get pods

NAME                 READY   STATUS    RESTARTS         AGE


nginx-prod            1/1     Running   1 (9m23s ago)    8d
```

- Apart from exploring a Pod externally, you can also connect to it and run commands on the primary container in a Pod:

`kubectl exec -it nginx-prod -- sh`

- The previous command will initiate an interactive shell session with the main container in the Pod.
- From here run any command to investigate
- Use exit to disconnect 

Now not all the Pods will contain all the command line utilities, therefore commands like `ps` may not work, usually when this happens you can go to the `proc (cd /proc)` folder and do an ls to see what commands are being run.

```
$ kubectl exec -it nginx-prod -n production -- sh

# ls

bin  boot  dev docker-entrypoint.d  docker-entrypoint.sh  etc home  lib  media  mnt  opt  proc  root run  sbin  srv sys  tmp  usr  var

# ps

sh: 2: ps: not found

# cd /proc
# ls

1   32 35  38 41  buddyinfo  cmdline   cpuinfo      devices   driver       filesystems  iomem    kallsyms keys     kpagecount  locks   modules  net self   stat   sysrq-trigger  timer_list  version   zoneinfo

30  33 36  39 42  bus        config.gz  crypto       diskstats  execdomains  fs     ioports  kcore kmsg     kpageflags  meminfo  mounts   pagetypeinfo  slabinfo  swaps  sysvipc tty     vmallocinfo

31  34 37  40 49  cgroups    consoles   device-tree  docker   fb       interrupts   irq      key-users kpagecgroup  loadavg misc   mpt   partitions softirqs  sys   thread-self uptime      vmstat

# cat 1/cmdline

nginx: master process nginx -g daemon off;# 

# exit
```

To get the information as shown in etcd you can use the following command

`get pods <Pod-Name> -o json`

To get the information in a more "readable way" you can use 

`get pods <Pod-Name> -o yaml`

From there if you are interested in learn more about a specific pod field (Kubernetes documentation provides details about several parameters of different resources), you can use the command 

`kubectl explain pods.spec.fieldName`

to get a description of what a field does as shown in the example below.

```
$ kubectl explain pods.spec.enableServiceLinks

KIND:       Pod

VERSION:    v1

  

FIELD: enableServiceLinks <boolean>

  

DESCRIPTION:

    EnableServiceLinks indicates whether information about services should be

    injected into pod's environment variables, matching the syntax of Docker

    links. Optional: Defaults to true.
```
## Pod Logs

- The Pod entrypoint application does not connect to any `STDOUT`
- Application output is sent to the Kubernetes cluster
- Use `kubectl logs` to connect to this output
- Using `kubectl logs` is helpful in trouble shooting

### Troubleshooting Failing Applications

- Start by using `kubectl get pods` and check the status of your application
- While seeing anything odd, use `kubectl describe pod <Pod-Name>` to get more information
- If the Pod main application generate a non-zero exit code, use `kubectl logs` to figure out what is going wrong

## Using port forwarding to access pods

- Pods can be accessed in multiple ways
- A very simple way is by using port forwarding to expose a Pod port on the kubectl host that forwards to the pod

`kubectl port-forward <Pod-Name> 8080:80`

- Port forwarding is useful for testing Pod accessibility on a specific cluster node, not to expose it  to external users
- Regular user access to applications is provided through services and ingress

To get the IP of the pod use the command

`kubectl get pods -o wide`
## Understanding Security Context

A `SecurityContext` defines privilege and access control settings for a Pod or container, and includes the following:
- Discretionary Access Control which is about permissions used to access an object
- Security Enhanced Linux, where security labels can be applied
- Running as privileged or unprivileged user
- Using Linux capabilities
- App Armor, which is an alternative to SELinux
- **Allow Privilege Escalation, which controls if a process can gain more privileges than its parent process**
- Notice that `SecurityContext` can be applied to pods as well as containers
- When `SecurityContext` prevents a pod from running successfully, use `kubectl describe` to get additional information from the events 
- In some cases, you will need to analyze in more depth and use `kubectl logs` on the failing Pod as well

## Managing Jobs

- Pods normally are created to run forever
- To create a Pod that runs up to completion use Jobs instead
- Jobs are useful for one-shot tasks, like backup, calculation, batch processing and more
- Use` spec.ttlSecondsAfterFinished` to cleanup completed Jobs automatically

There are 3 different Job Types can be started, which is specified by the **completions** and **parallelism** parameters: 
- **Non-parallel Jobs**: one Pod is started, unless the Pod fails
	- completions = 1
	- parallelism = 1
- **Parallel Jobs** with a fixed completion count: The job is complete after successfully as many time as specified in `jobs.spec.completions`
	- completions = n
	- parallelism = m
- **Parallel Jobs with a work queue**: multiple Jobs are started, when one completes successfully, the job is complete
	- completions = 1
	- parallelism = n

Commands related to jobs

| Command               | Description |
| :----------------  | :----: |
| `kubectl create job <Job-Name> --image=<Image-Name> -- Command`     | Create a Kubernetes Job named `<>Job-Name` using the image `<Image-Name>` and command `Command`|
| `kubectl get jobs `| List all the jobs running in the kubernetes cluster| 
| `kubectl delete job <Job-Name> `| Delete a specific Job Named `<Job-Name>`| 

To modify the job, you can do so by editing the Job's YAML file. See the example below:

```
kubectl create job myjob --image=busybox --dry-run=client -o yaml -- date
```

This will output the following YAML file

```
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: myjob
spec:
  template:
    metadata:
      creationTimestamp: null
    spec:
      containers:
      - command:
        - date
        image: busybox
        name: myjob
        resources: {}
      restartPolicy: Never
status: {}
```

You can add the parameters for `completions`, `parallelism`, and `ttlSecondsAfterFinished` within the `spec` section here:

```
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: myjob
spec:
  completions: 3
  parallelism: 2
  ttlSecondsAfterFinished: 60
  template:
    metadata:
      creationTimestamp: null
    spec:
      containers:
      - command:
        - date
        image: busybox
        name: myjob
        resources: {}
      restartPolicy: Never
status: {}
```
## Managing Cron Jobs

Cron Jobs are higher-level kubernetes objects that manages Jobs.  
- Cron Jobs schedule Jobs.
- Jobs when run initiate Pods.

- Jobs are used to run a task a specific number of times
- CronJobs are used for tasks that need to run on regular basis
- When running na Cronjob, a job will be scheduled
- This Job, on its turn, will start a Pod
- To test a CronJob, use:

```
kubectl create job <Job-Name> --from=cronjob/<Cron-Job-Name>
```

Below are listed more Cron Job related commands

|Command|Description|
|---|---|
|`kubectl create cronjob MyCronJob --image=ImageName --schedule=Schedule -- Command`|Create a Kubernetes CronJob named `MyCronJob` using the specified container image (`ImageName`), schedule (`Schedule`), and command (`Command`).|
|`kubectl create job MyJob --from=cronjob/MyCronJob`|Create a Job named `MyJob` using the settings from the `MyCronJob` CronJob.|
|`kubectl get cronjobs` List all the CronJobs in the Kubernetes cluster.||
|`kubectl logs MyCronJob-xxx-yyy`|View the logs of a specific CronJob instance, identified by `MyCronJob-xxx-yyy`.|
|`kubectl delete cronjob MyCronJob`|

## Managing Resource Limitations and Quota

- Resource requests and limits are set as an application property
- By default, a Pod will use as much CPU and memory as necessary to do its work
- This can be managed by using Memory/CPU **requests** and **limits** in `pod.spec.containers.resources`
- A **request** is an initial request for resources
- A **limit** defines the upper threshold of resources a Pod can use
- Memory as well as CPU limits can be used
- CPU limits are expressed in millicore or millicpu 1/1000 of a CPU core 
	- So, 500 millicore is 0.5 CPU
- When being scheduled, the kube-scheduler ensures that the node running the Pods has all requested resources available
- If a Pod with resource limits cannot be scheduled, it will show a status of Pending
- Use
```
kubectl set resources ...
```
- To apply resource limits to running applications in deployments 

Below we show an example of a Pod YAML file with resources configured

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: mynginx
  name: mynginx
spec:
  containers:
  - image: nginx
    name: mynginx
    resources:
      requests:
        cpu: "0.25"
        memory: 250Mi
      limits:
        cpu: "0.5"
        memory: 500Mi
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

- Quota are restrictions that are applied to namespaces
- If Quota are set on namespace, applications started in that namespace must have resource request and limits set
- Use
```
kubectl create quota ... -n <Namespace-Name>
```
to apply quota

For example to create a quota, you can use the following command: 

`kubectl create quota myquota -n restricted --hard=cpu=2,memory=1G,pods=3`.

or the YAML file

```
apiVersion: v1
kind: Namespace
metadata:
  creationTimestamp: null
  name: restricted
spec: {}
status: {}
---
apiVersion: v1
kind: ResourceQuota
metadata:
  creationTimestamp: null
  name: myquota
  namespace: restricted
spec:
  hard:
    memory: 1G
    cpu: "2"
    pods: "3"
status: {}
```

Quota restrictions will be visible when you describe the Namespace using `kubectl describe namespace restricted`:

```
Name:         restricted
Labels:       kubernetes.io/metadata.name=restricted
Annotations:  <none>
Status:       Active

Resource Quotas
  Name:     myquota
  Resource  Used  Hard
  --------  ---   ---
  cpu       0     2
  memory    0     1G
  pods      0     3
```

Resource creation will fail in the following scenarios:

- If a resource without resource limitations is created in a namespace with Quota.
- If a resource with resource limitations is created and it exceeds the Quota.

## Cleaning up Resources

- Generally resources are not automatically cleaned up
- Some resources have options for automatic cleanup if they're no longer used
- Periodic manual cleanup may be required
- If a Pod is managed by deployments, the deployment must be removed, not the Pod
- Try not to force resource to deletion, it may bring them in an unmanageable state
Below some resource related commands

|Command|Description|
|---|---|
|`kubectl delete all --all`|Delete all resources in the current namespace.|
|`kubectl delete all --all --force --grace-period=-1`|Forcefully and immediately delete all resources in the current namespace, bypassing any graceful termination periods. _**Note: Running this is not recommended, as it can be dangerous for your environment.**_|


## Lab 6

There are many ways to do this, i follow the next recipe

First created the namespace since is a 1 CLI command

```
kubectl create namespace secret
```

Then performed the following command

```
kubectl run secret-app -n secret --image=busybox --dry-run=client -o yaml -- sleep 3600  >> secret-app.yaml
```

Next i copied the resource code example in [Container resources example](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#example-1)


```yaml
resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

Finally i modified the `restartPolicy: OnFailure` From Always leaving the following YAML file below

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: secret-app
  name: secret-app
  namespace: secret
spec:
  restartPolicy: OnFailure
  containers:
  - args:
    - sleep
    - "3600"
    image: busybox
    resources:
      requests:
        memory: "64Mi"
      limits:
        memory: "128Mi"
    name: secret-app
    resources: {}
  dnsPolicy: ClusterFirst
status: {}
```
