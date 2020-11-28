# Enve Labs Training - Kubernetes
This directory contains a list of commands required to run a Kubernetes cluster in a single host on a virtualized environment.</br>

Please note that this process was successfully tested in macOS and Linux host systems, hopefully this will work also in Windows environments.

### Prerequisites

- VirtualBox (https://www.virtualbox.org) must be installed on your computer.
- Vagrant (https://vagrantup.com) must be installed on your computer.


we going to deploy a linux virtual machine through `Vagrant` with all the required packages in order to run `Docker` + `Kubernetes` and `Minikube` inside.  

### Environment creation
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


list pods

    sudo kubectl get nodes
