# Introduction to Kubernetes
Kubernetes is an orchestration tools that allow us to deploy a complex cluster in order to run containerized applications

### Deploying a K8s cluster
deploy your VM

    vagrant up

connect to the VM 

    vagrant ssh

start the minikube cluster
    
    sudo minikube start --driver=none

list nodes in the the minikube cluster
    
    sudo kubectl get nodes

