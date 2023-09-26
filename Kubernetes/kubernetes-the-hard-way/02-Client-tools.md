---
tags:
  - Kubernetes
---

### Install cfssl cfssljson

brew install cfssl

### Instal kubectl 

`curl -o kubectl https://storage.googleapis.com/kubernetes-release/release/v1.21.0/bin/darwin/amd64/kubectl

`chmod uga+wrx kubectl

`sudo mv kubectl /usr/local/bin/

#### Verifications

`cfssl version

`cfssljson --version

`kubectl version --client
