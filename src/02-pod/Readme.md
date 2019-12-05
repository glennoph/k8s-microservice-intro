## 02-pod 

* Deploy 2 pods with different labels
* Update the service from release 0 to release 0-5 to switch the pods

### Apply yml with 2 pods and switch update the service selector 
cd to src/02-pod
* `kubectl apply -f pod02a.yml`

check service

* `kubectl apply -f pod02b.yml`

check service (should see Release 0.5 changes)

#### pod02a.yml contents
[pod02a.yml](file:pod02a.yml)

- Pod : webapp 
  - label app:webapp release:0

- Pod : webapp-release-0-5 
  - label app:webapp release:0-5

- Service : fleetman-webapp 
  - selector:  app:webapp release:0
  - nodePort: 30080

#### pod02b.yml contents
[pod02b.yml](file:pod02b.yml)

- Pod : webapp 
  - label app:webapp release:0

- Pod : webapp-release-0-5 
  - label app:webapp release:0-5

- Service : fleetman-webapp 
  - selector:  app:webapp release:0-5
  - nodePort: 30080

### Access service 

* find minikube ip

`minikube ip`
  - could be 192.168.99.100

* service url

http://192.168.99.100:30080

  - should see map in browser
