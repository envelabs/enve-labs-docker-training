# Enve Labs Training - Docker Swarm
Docker Swarm is the native tool provided with the Docker Engine that allow us to create cluster of nodes that runs dockerized applications

This directory contains a list of commands required to run applications in docker swarm mode in a virtualized environment.</br>
Please note that this process was successfully tested in macOS and Linux host systems, hopefully this will work also in Windows environments.

### Prerequisites

- VirtualBox (https://www.virtualbox.org) must be installed on your computer.
- Vagrant (https://vagrantup.com) must be installed on your computer.


we going to deploy three linux virtual machines through `Vagrant` with all the required packages to run `Docker` inside and communicate these instances in order to build a Cluster of nodes


### Deploying a Docker Swarm cluster
deploy you VM

    vagrant up

connect to the first VM that will act as a manager

    vagrant ssh <manager-node>

### Create a Docker Swarm cluster
start docker in swarm mode

    docker swarm init


list nodes

    docker node ls

get more information about a node

    docker node inspect <node-id>


retrieve information from master node to join another node as a manager

    docker swarm join-token manager


retrieve information from master node to join another node as a worker

    docker swarm join-token worker


in the second and third instances run

    docker swarm join --token <join-token> <ip address>:2377


promote a node to `master`

    docker node promote <node2>


create a service

    docker service create <service-name> <image-name>


nginx example with params

    docker service create --name nginx -p 80:80 nginx:alpine


list running services

    docker service ls


list tasks (containers) from a service

    docker service ps <service-name>


service update

    docker service update --publish-add 8888 <service-name>

service scale

    docker service scale nginx=4


service update

    docker service --update-parallelism 2 -p 80:80 nginx:alpine


service image update

    docker service update --image <new-image>:<tag> <service-name>


service rollback

    docker service update --rollback --update-delay 0s <service-name>


checking logs

    docker service logs <service-name>

mount data volumes

    docker service create --mount type=volume,src=<vol-name>,dst=<container-path> --name <service-name> <image>


mount bind volumes

    docker service create --mount type=bind,src=<host-path>,dst=<container-path> --name <service-name> <image>


remove a running services

    docker service rm <service-name>


deploy a stack

    docker stack deploy -f <compose-file.yml> <stack-name>


list running stacks

    docker stack ls
