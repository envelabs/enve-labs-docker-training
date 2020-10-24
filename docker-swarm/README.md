# Enve Labs Training - Docker Swarm 
Docker Swarm is the native tool provided with the Docker Engine that allow us to create cluster of nodes that runs dockerized applications

### Deploying a Docker Swarm cluster
deploy you VM 

    vagrant up

connect to the VM 

    vagrant ssh

start docker in swarm mode for a single host

    docker init

list nodes

    docker node ls 

create a service
  
    docker service create <service-name>

list running services
  
    docker service ls

remove a running services
  
    docker service rm <service-name>

deploy a stack 

    docker stack deploy -f <compose-file.yml> <stack-name>

list running stacks

    docker stack ls

 

