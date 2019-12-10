## 04-replicaset

maintains set of replica pods such that specified number of pods are running

* Add queue and service for queue
* The service access release 0-5 pod

### Apply yml with queue
cd to src/03-queue

* `kubectl apply -f pods.yml services.yml`

  - apply pods.yml and services.yml

check service

#### pods.yml contents
[pods.yml](file:pods.yml)

- ReplicaSet
  - Pod : webapp-release-0-5 
  spec:
    template:
	  metadata:
	    labels:
		  app: webapp

- Pod : queue
  - label app:queue  image: k8s-fleetman-queue:release1
  - port: 8161 (admin console) expose port: 30010
    

#### services.yml contents
[services.yml](file:services.yml)

  - label app:queue  image: k8s-fleetman-queue:release1
  - port: 8161 (admin console) expose port: 30010
    	
	
- Service : fleetman-webapp 
  - selector:  app:webapp
  - nodePort: 30080

	
- Service : fleetman-queue 
  - selector:  app:queue
  - nodePort: 30010

### Access service 

* find minikube ip

`minikube ip`
  - could be 192.168.99.100

* service url

http://192.168.99.100:30080

  - should see map in browser


* service url queue

http://192.168.99.100:30010

  - ActiveMQ 
  - click Manage ActiveMQ broker link -- cred admin/admin
  

