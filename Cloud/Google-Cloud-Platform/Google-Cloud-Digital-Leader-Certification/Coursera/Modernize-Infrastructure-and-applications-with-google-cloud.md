---
tags:
  - GCP
  - GoogleCloud
  - Certification
---
## Important Cloud migration terms

### Workload 
- Specific application
- Service
- Capability

Workloads include
- Containers
- databases
- virtual machines
### Retired 

Retiring a workload is removing from the platform due to several reasons
- obsoleted
- Unnecessary
- Not cost-effective
- not secure
- not compatible with a specific platform
### Retained 

Intentionally kept workloads
- - On-premises
- kept in a hybrid cloud environment
- managed by the business
- Not subject to the same level of cloud provider control
### Rehosted 
- Refers to migrating a workload in the cloud without change of code
- Lift and shift
- managing workloads Can be difficult
### Replatform
- Move and improve
- change code so it can be run in the cloud
- scalability
- reliability
- cost-effective
- can be complex and time-consuming
### Refactored
- change code of a workload
- more efficient scalable and secure
- can be complex and time-consuming
### Reimagined
- rethinking change then cloud strategy
- AI
- machine learning
## Modernizing infrastructure in the cloud

### The benefits of running compute workloads in the cloud

- Total cost of ownership (TCO)
	- Initial purchase
	- maintenance
	- operation
	- other associated costs

Cloud providers offer
- pays as you go, model,
- long term commitment discounts
- Scalability
- Reliability
- Security
	- Data encryption
	- identity and access management
	- network security
	- virtual private clouds
	- monitoring services
- Flexibility
- abstraction
### Virtual machines

Is a form of resource optimization that lets multiple systems run on the same hardware

Systems are virtual machines
This mean they share the same 
- pool of processing
- storage
- networking resources
#### Compute engine
Is Google's cloud Infrastructure as a Service (IaaS) service product
that lets run virtual machines on google infrastructure
- no upfront investments
- Thousands of virtual CPUs can run on a system that's designed to be fast and to offer consistent performance
- Each VM contains the power and functionality of a full-fledged operating system
- can be configured much like a physical server by specifying
	- The amount of CPU power and memory needed
	- the amount and type of storage needed
	- the operating system
####  Virtual machine creation
- Google Cloud Console which is a web-based tool to manage Google Cloud projects and resources
- Google Cloud CLI by using infrastructure automation tools such as Terraform or the compute engine API
#### API
A set of instructions that allows different software programs to communicate with each other


- bills by the second
- 1-minute minimum
- sustained-use discounts
- committed use discounts
- preemptive and spot vms
	- needs to ensure job can be stop

| Spot VMS    | PREEMPTIBLE VMS |
| -------- | ------- |
| More features  | Less features    |
| No maximum runtime| Runtime up to 24h|

Compute engine lets you choose the machine properties
- Number of virtual CPUs
- Operating system
- Amount of memory
by 
- Using a set of predefined machine types
- creating system machine types
### containers

Virtual machines virtualize an entire machine down to the hardware layers

Containers virtualize software layers above the operating system level

A container is packaged with your application and all of its dependencies so it has everything to run.
- independently developed
- independently tested
- independently deployed
- well suited for a microservices-based architecture

Containerized applications
### managing containers

Kubernetes, originally developed by Google, is an open-source platform for managing containerized workloads and services. 

It makes it easy to orchestrate many containers on many hosts, scale them, and easily deploy rollouts and rollbacks.

GKE - Google hosted managed Kubernetes service in the cloud
GKE environment consists of multiple machines, specifically compute engine instances grouped to form a cluster.

Support
- Different machine types
- number of nodes
- network settings

GKE Provides API and Web console

Google Kubernetes Engine - Autopilot
- A mode that enables full management of an entire cluster's infrastructure and provides per-pod billing

Eliminate the need to configure and monitor clusters
Only pay for running pods

**Cloud run**

fully managed serverless platform to deploy and run containerized applications without the need to worry about the underlying infrastructure

GKE provides lots of control over a Kubernetes environment with complex applications to run}
Cloud run - A simple fully managed serverless platform that can scale up and down quickly
### Serverless computing

At its simplest definition, serverless means that businesses provide the code for whatever function they want and the public Cloud provider does everything else.

Function as a service

#### Cloud run
- A fully managed environment for running containerized apps
#### Cloud functions
- A platform for hosting simple single-purpose functions that are attached to events emitted from your cloud infrastructure and services
#### Service to build and deploy web applications

- Reduce operational costs
- Scalability
- Faster time to market
- Reduced development costs
- improved resilience
- pay-per-use pricing model

### The benefits of modern cloud application development

With model cloud applications software is now
- Flexible
- Scalable
- Uses the latest technologies

- **Monolithic applications**
	- Required application components to be developed and deployed as a single, tightly coupled unit, typically using a single programming language

A**rchitecture**

Modern cloud applications are typically built as a collection of microservices

**Deployment**
- Managed services take care of the day-to-day management of cloud-based infrastructure, such as:
	- Patching 
	- Upgrades
	- Monitoring

**Scalability**
- modern cloud-based applications can easily be scaled up or down to meet user demands

**Highly available and resilient**
- Load balancing: Distributing network traffic evenly across multiple servers that support an application
- Automatic failover Allows a cloud-based application to automatically switch to a backup server id a failure occurs

Monitoring and management tools
- Allows developers to quickly identify and respond to issues
#### Rehosting legacy applications in the cloud

Lift and shift
- Cost savings
- Scalability
- Reliability
- Security

Complexity, Risk, Vendor lock-in

Google Cloud VMware Engine

Big query, AI/ML Google Kubernetes Engine

Bare Metal Solution

A fully managed cloud infrastructure solution, that lets organizations run their oracle workloads on dedicated, bare metal servers in the cloud
### API - Application Programming Interfaces

An API is a set of instructions that lets different software programs communicate with each other.

Using APIs can create new business opportunities for organizations and improve online experiences for users

- Can be used to create new products and services
- Can be used to generate new revenue streams
- Can create partnerships
#### API Management

APIgee API Management 
- google cloud's API management service to operate APIs with enhanced scale, security and automation

- Help organizations to secure their APIs
- tracks and analyzes API usage
- It helps with developing and deploying APIs
- It offers API versioning, API documentation, and even API throttling

AccuWeather
- API
- Global partners

API -> Individual developers
### Hybrid and multi cloud

- Compliance concerns

Hybrid 
- On premises and google cloud
- Private cloud and google cloud interconnection

Multicloud

This lets organizations
- Keep parts of the system infrastructure on-premises while they move other parts to the cloud
- Move only specific workloads to the cloud
- benefit from the flexibility scalability and lower computing costs
- Add specialized services to the organization's computing resources toolkit

GKE enterprise

A production-ready platform for running Kubernetes applications across multiple cloud environments
- Multicloud and hybrid-cloud support
- Centralized management
- Security and compliance
- Networking and load balancing
- Monitoring and logging
