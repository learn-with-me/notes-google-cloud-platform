# Kubernetes

#### Components

* etcd - distributed key-value data store
* Kubernetes Master - connects to etcd via HTTP/HTTPS to store data
* Kubernetes Nodes - connects to Kubernetes Master via HTTP/HTTPS to get a command and report status
* Kubernetes Network

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

### Tools

#### kubectl

kubectl is used to connect through the hypervisor, to control Kubernetes.

#### minikube

minikube runs Kubernetes on the Linux VM on macOS. It relies on a hypervisor \(virtualization technology\), such as VirtualBox, VMWare fusion, or hyperkit.

With minikube, you can run the entire suite of the Kubernetes stack on macOS, including the Kubernetes master, node, and CLI. It is recommended that macOS has enough memory to run Kubernetes. By default, minikube uses VirtualBox as the hypervisor.

### Setting up Kubernetes Cluster via Ansible

If you are familiar with configuration management, such as Puppet, Chef and Ansible, kubespray is the best choice to set up a Kubernetes cluster from scratch. It provides the Ansible playbook that supports the majority of Linux distributions and public clouds, such as AWS and GCP.

Ansible is a Python-based SSH automation tool that can configure Linux as your desired state based on the configuration, which is called playbook. Here is how to use kubespray to set up Kubernetes on Linux.

Before you start, here are couple of ports that you'll need to open for communication

* TCP/22 \(ssh\) - Ansible to Kubernetes master/node host
* TCP/6443 \(Kubernetes API Server\) - Kubernetes node to master
* Protocol 4 \(IP encapsulated in IP\) - Kubernetes master and node to each other by Calico
  * AWS
    * aws ec2 authorize-security-group-ingress --group-id &lt;your SG ID&gt; --cidr &lt;network CIDR&gt; --protocol 4
  * GCP
    * gcloud compute firewall-rules create allow-calico --allow 4 --network &lt;your network name&gt; --source-ranges &lt;network CIDR&gt;

Installation

```
$ sudo pip install ansible
$ which ansible
$ ansible --version

$ sudo pip install netaddr

# Download kubespray from https://github.com/kubernetes-incubator/kubespray/tags
# Unzip and cd into the directory
```

### Setting up ssh public key authentication

Ansible is actually the ssh automation tool. If you log on to host via ssh, you have to have an appropriate credential \(user/password or ssh public key\) to the Kubernetes master and nodes. Due to security reasons, especially in the public cloud, Kubernetes uses only the ssh public key authentication instead of ID/password authentication.

```
$ ssh-keygen -q                # create an ssh public/private key pair
$ cat .ssh/id_rsa              # Show RSA Private key

// use ssh-agent to remember your private key and passphrase (if you set)
$ ssh-agent bash
$ ssh-add

// logon from ansible machine to k8s machine which you copied public key
$ ssh 10.128.0.2
```



