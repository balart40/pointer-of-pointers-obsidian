---
tags:
  - GCP
  - GoogleCloud
  - Certification
---
## Security terms and concepts

### Privileged access

Grants specific users access to a broader set of resources than ordinary users
### Least Privilege

Advocates granting users only the access they need to perform their job responsibilities
### Zero trust architecture

Assumes that no user or device can be trusted by default
### Security default

Emphasizes integrating security measures into systems and applications from the initial stages of development
### Security Posture

The overall security status of a cloud environment 
### Cyber resilience

An organizations's ability to withstand recover quickly from cyber attacks
- Identifying, assessing, mitigating risks, responding to incidents effectively, and recovering from disruptions quickly.
# Security Measures

### Firewall

A network device that regulates traffic based on predefined security rules
### Encryption

The process of converting data into an unreadable format by using an encryption algorithm
## Decryption

Uses an encryption key to restore encrypted data back to its original form
# Cloud security components

### Confidentiality

Is about keeping important information safe and secret. It ensures that only authorized people can access sensitive data, not matter where it's stored or sent.
### Integrity 

Ensures that information doesn't get changed or  corrupted no matter where it's stored or how it's move around.

Involves the accuracy and trustworthiness of data
- checksums, etc
### Availability 

Ensure cloud systems are always ready to use by the right people when needed.
### Control

The measures and processes implemented to manage and mitigate security risks
- robust authentication mechanisms
- access restrictions 
- security awareness training
### Compliance

Relates to adhering to industry regulations, legal requirements, and organizational policies.
# Cloud security versus traditional on-premises security

## Location

Cloud security involves hosting  and managing data and applications in off site data centers  operated by cloud service providers. The responsibility for securing the infrastructure and underlying hardware lies with the cloud provider.  

Conversely, traditional on premises security involves hosting and managing data and applications locally on an organization's own servers and infrastructure, granting direct control and responsibility for securing the physical and virtual environment.
## Responsibility

**Cloud service provider** is responsible for securing:
- Infrastructure, network and physical facilities
**Customer**
- Data, applications, user access, configuration

**On premises**
 The organization is responsible for securing the entire infrastructure, including 
 - Hardware
 - Network
 - Operating Systems
 - Applications
 - Data
## Scalability

Cloud providers
- scalability
- elasticity

Organizations
- Are required to provision and maintain their own infrastructure
## Maintenance and updates

**Cloud service providers**
handle infrastructure maintenance, including:
- security updates
- patching
- software upgrades

On premises organizations
Maintain and update their own infrastructure involving regular tasks such as:
## Capital expenditure

Cloud
Follows an operational expenditure (OPEx) model, where organizations pay for the services they consume on a subscription basis

On premises 
Significant expenditure (Capex) because organizations must purchase and maintain their own security infrastructure 

**Cloud provides**
- Offloading infrastructure management
- scalability
- cost flexibility

On prem
- Direct control over the entire infrastructure 
- Data sensitivity
- compliance regulations
- scalability

# Cyber security

### Social engineering
### Physical damage

### Malware, viruses, and ransomware

### Vulnerable third-party systems

### Configuration mishaps

# Data centers

- Purpose built servers
- advanced networking solutions
- custom security hardware and software
### Zero trust architecture

Our custom hardware and software are purpose built with features like:
- Tamper-evident hardware
- secure boot
- hardware-base encryption 

Robust access control measures
Biometric authentication in place

**PUE**: Power Usage Effectiveness
# Secure storage

Data at rest
- Encryption at rest

Authenticity
Integrity
Privacy 

Memory encryption

Advanced Encryption Standard AES
### Authentication
- It serves as a gatekeeper because it verifies the identity of users or systems that seek access. 
- Authentication involves presenting unique credentials, such as passwords, physical tokens, or biometric data, like fingerprints or voice recognition

Two-step, two factor authentication
### Authorization

Access control mechanism

Admin

Standard user
### Auditing

Security Incidents Investigation
Compliance tracking
System performance evaluation

Identity and Access Management   IAM

Fine grained access control
Enhanced visibility
Centralized resource management
# Network security

Google cloud beyondcorp

DDos 
Distributed denial of service

Terraform
Jenkins
Cloud build
# Network security

Vulnerability management, is the process of identifying and  fixing security vulnerabilities in 
Cloud infrastructure and applications.

SCC
Security Command Center

Log mangement

# Google Trust principles and compliance

## The google cloud trust principles and transparency reports

- you own your data not google
- google does not sell customer data to third parties
- google cloud does not use customer data for advertising
- All customer data is encrypted by default
- We guard against insider access to your data
- we never give any government entity backdoor access
- our privacy practices are audited against international standard
## Data residency and data sovereignty 

**Data sovereignty:**
Refers to the legal concept that data is subject to the laws and regulations of the country where it resides

General Data Protection Regulation (GDPR)

**Data residency**
Refers to the physical location where data is stored or processed

Cloud Armor

## Industry and regional compliance

Google Cloud Resource Center
HIPAA Regulations

## Operational Excellence and Reliability at Scale

- Designing robust infrastructure
- Designing resilient processes
- Employing proactive monitoring and response mechanisms

**Operational Excellence**
- Efficiently scaling the underlying infrastructure
- Automating resource provisioning
- Implementing load balancing mechanism

**Reliability at Scale**
- Minimizing downtime
- Employing fault-tolerant systems
- Employ disaster recovery strategies
### Fundamentals of cloud reliability

**Developers**
- Are expected to be agile
- Are often pushed to write and deploy code quickly
- Aim to release new functions frequently
- Increase core business value with new features
- Release fixes fasts

**Operators**
- Are expected to keep the system stable
- Often prefer to work more slowly to ensure reliability and consistency

**SRE - Site Reliability Engineer**
- Ensures reliability, availability and efficiency of software systems and services deployed in the cloud

**Monitoring**
- Reveals what needs urgent attention
- Shows trends in application usage patterns
- Can yield better capacity planning
- Help improve an application client's experience

#### 4 Golden signals for a system performance and reliability

1. **Latency**
	1. Measures how long it takes for a particular part of a system to return a result
		1. It directly affects the user experience
		2. changes in latency could indicate emerging issues
		3. Its values might be tied to capacity demands
		4. It can be used to measure system improvements
2. **Traffic**
	1. Measures how many requests reach your system
		1. It's an indicator of current system demand
		2. its historical rends are used for capacity planning
		3. It's a core measure when calculating infrastructure spend
3. **Saturation**
	1. How close to capacity a system is
		1. Its an indicator of how full the service is
		2. it focuses on the most constrained resources
		3. It's frequently tied to degrading performance as capacity is reached
4. **Errors**
	1. Are events that measure system failures or other issues often raised when a flaw, failure or fault in a computer program or system causes it to produce incorrect or unexpected results or behave in unintended ways.
		1. They may indicate that something is failing
		2. they may indicate configuration or capacity issues
		3. they can indicate service level objective violations
		4. an error might mean its time to send out an alert

#### Service Level indicator
- Measurements that show how well a system or service is performing
- They're specific metrics like
	- response time
	- error rate
	- percentage uptime
#### Service level objectives
- Goals that we set for a system's performance based on SLIs
- Define what level of reliability or performance that we want to achieve
	- System should be available 99.9% of the time in a month
#### Service level agreements
- Agreements between a cloud service provider and its customer
- They outline the promises and guarantees regarding the quality of service
- SLA include the agreed-upon SLOs performance metrics, uptime guarantees, and any penalties or remedies if the provider fails to meet those commitments
### Designing resilient infrastructure and processes

#### High Availability
- The ability of a system to remain operational and accessible for users even if hardware or software failures occur
#### Disaster recovery
- The process of restoring a system to a functional state after a major disruption or disaster

**Redundancy** 
- Refers to duplicating critical components or resources to provide backup alternatives

**Replication**
- Involves creating multiple copies of data or services and distributing them across different servers or locations

**Regions**
- Cloud service providers offer multiple regions or data center locations spread across different geographic areas

**Scalable infrastructure**
- Building a scalable infrastructure allows organizations to handle varying workloads and accommodate increased demand without compromising performance or availability

**Backus**
- Regular backups or critical data and configurations are crucial to ensure that if data loss, hardware failures, or cyber-attacks occur, organizations can restore their systems to a previous state
### Modernizing operations by using google cloud

Using google cloud observability tools
- Involves collecting, analyzing and visualizing data from various sources within a system to gain insights into its performance, health and behavior
#### Cloud Monitoring
- Provides a comprehensive view of cloud infrastructure and applications
- Collets metrics, logs, and traces from applications and infrastructure, and provides insights into their performance, health and availability 
- Lets you create alerting policies to notify when metrics, health check results and uptime checks results meets the  specific criteria
#### Cloud Logging
- Collects and store all application and infrastructure logs
- Real-time insights to help you troubleshoot issues identify trends and comply with regulations
#### Cloud Trace
- Helps identify performance bottle necks in applications
- Collects latency data from applications and provides insights into how they are performing
#### Cloud Profiler
- Identifies how much CPU power memory and other resources application uses.
- Continuously gathers CPU usage and memory allocation information from production applications.
- Provides insights into how applications are using resources
#### Error reporting
- Counts analyses and aggregates the crashes in running cloud services in real-time
- A centralized error management interface displays the results with sorting and filtering capabilities
- A dedicated view shows
	- Time chart
	- ocurrences
	- affected user count
	- first-and last seen dates
	- cleaned exception stack-trace
- Supports email and mobile alerts notification through its API
### Google cloud customer care
- Basic
- Standard
- Enhanced
- Premium
### The life of a support case
- Case creation
- case triage 
- case assignment
- trouble shooting and  investigation
- Communication and updates
- escalation
- Resolution and mitigation
- validation and testing
- case closure
- 

