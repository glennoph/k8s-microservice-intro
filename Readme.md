# k8s-microservice-intro
## video
[Kubernetes Microservices by R Chesterwood](https://livevideo.manning.com/course/80/kubernetes-microservices)
## Install
### Install kubectl
[k8s install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

`sudo snap install kubectl --classic`

### Install minikube
[k8s install minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)

* install hypervisor, eg, VirtualBox
* Download from github and install via apt

* version :: `minikube version`
* status  :: `minikube status`

```
Package: minikube
Version: 1.5.2
Maintainer: Thomas Strömberg <t+minikube@stromberg.org>
Recommends: virtualbox
```
## Pod Intro
> Collection of multiple containers that share storage and networking
* "a wrapper for a container"
* multiple containers in a pod ... main container and helper container
### Pod API Reference
* how to create a pod via yml file
[k8s api reference](https://kubernetes.io/docs/reference/#api-reference)
[pod v1 core](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.16/#pod-v1-core)

```yml
apiVersion: v1
kind: Pod
metadata:
  name: pod-example
spec:
  containers:
  - name: ubuntu
    image: ubuntu:trusty
    command: ["echo"]
    args: ["Hello World"]
```
### First Pod deploy
Source: [src/pod01.yml](src/pod01.yml)
* Start VirtualBox 
* k8s status :: `minikube status` ... should be Running

* Deploy first pod :: `kubectl apply -f src/pod01.yml`

* Get all pods :: `kubectl get all`

* Describe pod :: `kubectl describe pod webapp`

* Shell to pod :: `kubectl -it  exec webapp sh`

## Services
Pods are cattle, short lived.

Services are long lived.

* Selector of a service connects to pod via label on pod 

### Service API Ref
* [Service v1 core example](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.16/#service-v1-core)

* See [src/pod01-service.yml](src/pod01-service.yml)

* apply service :: `kubectl apply -f src/pod01-service.yml`
* also add label to the webapp
* apply webapp :: `kubectl apply -f src/pod01.yml`

* find the ip
`minikube ip`

* access page http://192.168.99.100:30080/ ... displays map

#### reconfig minikube
* large
```
minikube delete
minikube start --cpus=4 --memory=4096
```
* medium
```
minikube delete
minikube start --cpus=6 --memory=8192
```
* retest  http://192.168.99.100:30080/ ... ok
