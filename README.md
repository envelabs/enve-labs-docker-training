# Docker
A container technology is a method to package an application with all its dependencies isolated from other processes. </br>
Docker containers images are lightweight, standalone, executable packages of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.</br>

Container images become containers at runtime and in the case of Docker containers - images become containers when they run

### Components
Docker has three essential components

- Docker Engine
- Docker Client (tools)
- Docker Registry

Docker Engine provides the core capabilities for container management. It interfaces with the underlying operating system exposing an API to handle the lifecycle of containers.

Docker Client is a set of command line tools that interact with the API exposed by the Docker Engine. They are used to run containers, manage images, configure storage and networks, among other operations that impact the lifecycle of a container.

Docker Registry is a place where container images are stored. Each image can have multiple versions identified through tags that are pulled by users the first time that they `run` a container image. Docker Hub (https://hub.docker.com/) is a free hosted registry managed by Docker, Inc. It is also possible to run a registry within your own infrastructure to keep the images in a private/secure environment.

### Installation
the following commands will remove any existing docker-related packages that might already be installed and then install Docker from the official repository
```
sudo apt-get remove docker docker-engine docker.io
sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates software-properties-common curl jq
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
```

Validate the installation
```
docker info
```

Show the information relative to the version installed
```
docker version
```

### Running a Container
Docker containers are executed based in existing images which are stored in private or public registries. Private registries/repositories require users to authenticate before pulling images. Public images can be accessed by anyone. By default, Docker search for images in hub.docker.com. </br>

To search for an image named hello-world in a public repository, run the command:
```
docker search hello-world
```

List local images available
```
docker images
```

Download an image from a public repository
```
docker pull hello-world
```

Run a docker container using the `hello-word` image
```
docker run hello-world
```

Run a specific instance of an image with options
```
docker run -p 80:80 --name webserver -d httpd
```

  - `-p` - This option tells Docker Engine to expose the container's port 80 on the host's port 80. Since Apache webserver listens on port 80, we need to expose it on the host port. </br>
  - `--name` - This option assigns a name to our running container. If we omit this, Docker Engine will assign a random name.</br>
  - `-d` - This option instructs Docker Engine to run the container in detached mode. Without this, the container will be executed in foreground, blocking access to the shell. Pushing the container into the background, we can continue to use the shell session used to run the container while the container is still running.


List running containers
```
docker ps
```

List all available containers (including the stoped/exited)
```
docker ps -a
```

Stop a running container
```
docker stop <container_id|container_name>
```

Remove a container
```
docker rm <container_id|container_name>
```

Remove an exited container
```
docker ps --no-trunc -aqf "status=exited"| xargs docker rm
```

### Docker Networking
Create network
```
docker network create <network_name>
```

List networks
```
docker network ls
```

Run a container with specific IP
```
docker run -it --rm -p 10.0.0.99:8080:8080 <docker_image>
```

Change DNS
```
sudo dockerd --dns=10.9.10.12
```

### Docker Registry

Login against the `hub.docker.com` registry
```
docker login --username=<username>
```

Push an image to the repository
```
docker push <username>/<iamge>:<version>
```
