# Networking Docker
list docker networks
    
    docker network ls

create a docker network
  
    docker network create <network_name>

run a container with specific IP

    docker run -it --rm -p 10.0.0.99:8080:8080 <docker_image>

change DNS
  
    sudo dockerd --dns=10.9.10.12
