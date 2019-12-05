## 01-pod 

### Start minikube & check for pods
```
minikube start
kubectl get pods
```
* delete any pods/services, then deploy pod and service

### Apply 
cd to src/01-pod

`kubectl apply -f .`

#### pod01.yml contents
[pod01.yml](file:pod01.yml)

- Pod : webapp 
  - label app:webapp
- Service : fleetman-webapp 
  - nodePort: 30080


### Access service 

* find minikube ip

`minikube ip`
  - could be 192.168.99.100

* service url

http://192.168.99.100:30080

  - should see map in browser
