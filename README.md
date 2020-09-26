# Enve Labs Docker Training
A container technology is a method to package an application with all its dependencies isolated from other processes. </br>
Docker containers images are lightweight, standalone, executable packages of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.</br>
Docker images become containers at runtime.

### Components
Docker has three essential components

- Docker Engine
- Docker Client (tools)
- Docker Registry

Docker Engine provides the core capabilities for container management. It interfaces with the underlying operating system exposing an API to handle the lifecycle of containers.

Docker Client is a set of command line tools that interact with the API exposed by the Docker Engine. They are used to run containers, manage images, configure storage and networks, among other operations that impact the lifecycle of a container.

Docker Registry is a place where container images are stored. Each image can have multiple versions identified through tags that are pulled by users the first time that they `run` a container image. Docker Hub (https://hub.docker.com/) is a free hosted registry managed by Docker, Inc. It is also possible to run a registry within your own infrastructure to keep the images in a private/secure environment.

### Installation
the following commands will remove any existing docker-related packages that might already be installed and then install Docker from the official repository against a `debian` kind linux system

    sudo apt-get remove docker docker-engine docker.io
    sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates software-properties-common curl jq
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo apt-key fingerprint 0EBFCD88
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt-get update
    sudo apt-get install -y docker-ce

validate the installation

    docker info

show the information relative to the version installed
    
    docker version

