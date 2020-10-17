# Networking Docker
list docker networks

    docker network ls

create a docker network

    docker network create <network-name>

inspect the docker network

    docker network inspect <network-name>

run a container inside an specific network

    docker run --name c1 --hostname c1 -it --network net1 ubuntu bash

    docker run --name c1 --hostname c1 -dit -p 80:80 --network bridge nginx

connect a container to a network

    docker network connect <network-name> <container-name>

connect a container to 2 networks

    docker network create --driver=bridge net1 --subnet=172.19.0.0/24
    docker network create --driver=bridge net2 --subnet=172.19.1.0/24

running containers in a specific port

    docker container run --publish 80:80 -dit nginx
    net-tools


run a container with specific IP

    docker run -it --rm -p 10.0.0.99:8080:8080 <docker-image>

change DNS

    sudo dockerd --dns=10.9.10.12
