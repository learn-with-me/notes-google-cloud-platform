# Kubernetes

#### Components

* etcd - distributed key-value data store
* Kubernetes Master - connects to etcd via HTTP/HTTPS to store data
* Kubernetes Nodes - connects to Kubernetes Master via HTTP/HTTPS to get a command and report status
* Kubernetes Network

##### Node's Daemon processes for cluster

* kubectl
* kube-proxy

#### Kubernetes Master's functionalities

* Authorization and Authentication
* RESTful API entry point
* Container deployment scheduler to Kubernetes nodes
* Scaling and Replicating controllers
* Reading the configuration to setup the cluster

##### Daemon processes forming Master's functionality

* kube-apiserver - hub between kubernetes components
* kube-scheduler - helps to choose which container runs on which nodes
* kube-controller-manager - performs cluster operations

#### Kubernetes Node

kubelet is the main process on the Kubernetes node that communicates with the master to handle following operations:

* Periodically access the API controller to check and report
* Perform container operations
* Runs the HTTP server to provide simple APIs

kube-proxy handles the network proxy and load balancer for each container. It changes Linux iptables rules to control TCP and UDP packets across the containers. After starting the kube-proxy daemon, it configures iptables rules.



