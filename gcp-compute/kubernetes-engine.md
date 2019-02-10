# Kubernetes Engine \(GKE\)

Considered as the backbone of container orchestration. Kubernetes is a container orchestration technology, which adds a layer of abstraction that makes it easier for you to deploy and manage thousands of containers.

##### Node Pool

A subset of node instances, which have the same configuration are called node pools. GKE has a default node pool. You can add you custom node pools, with specific configurations. For example, there can be one of the node pool with high memory to serve memory requirements.

##### Node Images

GCP provides special operating system images, that are tuned to run on Kubernetes nodes.

* Container-optimized OS
* Container-optimized OS with `containerd` runtime
  * containerd contains the core components of docker runtime
* Ubuntu

##### Pods

Isolation units that Kubernetes uses to run containers. Isolation unit is a pod. One or more containers run on a single Node. Each container has a Docker container that is wrapped in a Pod object. Each pod can be made up of one or more docker containers. A pod can be thought of as a sandbox environment for containers. All the containers are managed using Kubernetes Master \(Control plane\).

Pods are atomic units that Kubernetes works with. They are the lowest level of abstraction around a container. When you deploy containers to your cluster, all of the Docker containers within a pod are deployed altogether or none of them are. A pod also offers node association, which means, all of the containers within the pod are deployed on the same node.

* You cannot run a docker container on a Kubernetes cluster without an enclosing pod
* Pods provide isolation between containers, so when containers within a pod crash, they do not affect containers running on other pods.
* Multiple containers within a pod are not recommended since they are tightly coupled except in advanced use cases.
* Pods are automatically assigned unique IP addresses.
* Pods can specify shared storage volume

For each container running in the pod

* Pod specification specifies the container image along with the source repository
* Also port on which container will be available

###### Pod Lifecycle

* Pending State
  * Request accepted, but not yet fully created
* Running State
  * Pod bound to node, all containers started
* Succeeded State
  * All containers terminated successfully and gracefully \(will not be restarted\)
* Failed State
  * All containers have terminated, and at least one failed.
* Unknown State
  * Pod status could not be queried

Standalone Pod Limitation

* No autohealing
  * Crashed pods won't restart automatically
* No scaling or autoscaling
  * Overloaded pods don't spawn more automatically
* No load balancing
  * Pod IP addresses are ephermal \(which means they can't be exposed as external endpoints\)
  * Pods can't share load automatically
* As compared to standalone containers, Pods do sandbox/isolate containers.

##### Objects

Kubernetes does not directly interact with the containers. Instead it uses a number of higher-level entities/abstractions referred to as objects. There are replicaset objects, service objects, deployment objects, ingress objects, etc

Every object is associated with a specification file \(YAML or JSON\) which represents the desired end state of the object. You usually do not interact with these files, but more with web console or gcloud commands. When you interact with the kubernetes cluster, there is a default state of every object. Controllers in the cluster run reconciliation loops to get the actual state to match the desired state.

When you're using raw Kubernetes cluster, that is when you work a lot explicitly with these configuration files. When you use GKE, you're completely abstracted away from the details of these specification files. In the latter case, you use web console or the gcloud command line utility.

#### Higher-level Abstraction

To offer all the features in a cluster, Kubernetes uses:

##### ReplicaSet, ReplicationController

* Scaling and healing for pods
* Multiple copies of pod are managed together using a ReplicaSet
* If pod crashes, ReplicaSet will start a new one
* A ReplicaSet object will govern all pods that match its label selector
* You never deal with ReplicaSets

##### Deployment

* Works with ReplicaSets to add Versioning and rollbacks and other advanced deployment functionality
* Triggers creation of new ReplicaSet and new containers
* Pods in old ReplicaSet gradually reduced to zero
* Each new deployment is a new revision, which is how GKE makes it trivial to make the rollbacks easy
* You can use Horizontal Pod Autoscaler with deployment as target
* Can pause/resume deployments midway
* Monitor status of your deployment
* You do deal with Deployment objects

##### Service

* Static \(non-ephermal\) IP addresses
* Stable networking
* Connects external clients to a set of back-end pods
* Containers expose ports in pod specification file

##### Persistent volumes

* Non-ephermal storage
* Defined in pod specification file
* Have each container mount volume independently

#### Important features by Kubernetes as Orchestrator

##### Fault tolerance

* Recover from pod or node failures

##### Autohealing

* Crashed containers restart

##### Scaling

* ReplicaSets for multiple copies of the pod

##### Autoscaling

* Scale up or down based on load
* Horizontal pod autoscalers

##### Isolation

* Containers run inside pods

##### Load balancing

* Made up of stable front-end IP address
* Has forwarding rules to funnel traffic
* Is connected to a backend service, which manages a number of nodes or instances
* Distributes load intelligently
* Typically uses health check to avoid unhealthy instances
* When you use deployment or service objects, you can configure load balancers to distribute traffic across containers

##### Other tasks handled by Kubernetes

* Handling master node
* Handling worker nodes
* Job scheduling
* Resource allocation
* Comparing actual and desired state by running reconciliation loops



