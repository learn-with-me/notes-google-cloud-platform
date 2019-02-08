# Kubernetes Cheatsheet

`gcloud` is Cloud SDK which is a set of tools for cloud platform

```
$ gcloud components list
$ gcloud components update
$ gcloud components install <componentID>
$ gcloud components remove <componentID>

$ gcloud bigtable instances list

$ gcloud functions list

$ gcloud config set project <project_id>
$ gcloud config list
$ gcloud app deploy

# Enabling services
$ gcloud services enable cloudkms.googleapis.com
```

You can use kubectl command to control the cluster

```
$ kubectl version --short       # kubectl version
$ kubectl get cs                # returns status of each component
$ kubectl get nodes             # returns a list of nodes
```

##### Basic Setup on local machine

```
$ brew install kubernetes-cli           # Install kubectl
$ brew cask install minikube            # Install minikube
$ open -a Docker.app                    # start Docker

Kubectl configuration can be found at ~/.kube/config
```

minikube

```
$ minikube start
$ cat ~/.kube/config
$ minikube stop
$ minikube delete
$ minikube ssh
$ minikube ip
$ minikube update-context
$ minikube dashboard
```



