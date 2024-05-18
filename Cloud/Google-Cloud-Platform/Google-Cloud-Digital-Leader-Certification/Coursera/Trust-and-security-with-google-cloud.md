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
