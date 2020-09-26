# Docker
This directory contains a list of commands required to run an application inside a docker container in a virtualised environment.</br>
Please note that this process was successfully tested in macOS and Linux host systems, hopefully this will work also in Windows environments.

### Pre requisites

- VirtualBox (https://www.virtualbox.org) must be installed on your computer.
- Vagrant (https://vagrantup.com) must be installed on your computer.


we going to deploy a linux virtual machine through `Vagrant` with all the required packages in order to run `Docker` inside.  

#### Environment creation:
Deploy the VM with all the required packages
```
vagrant up
```

Connect to the VM in order to work with Docker
```
vagrant ssh
```

Clean up when you're done
```
vagrant destroy
```

### Running a Container
Docker containers are executed based in existing images which are stored in private or public registries. Private registries/repositories require users to authenticate before pulling images. Public images can be accessed by anyone. By default, Docker search for images in https://hub.docker.com. </br>

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
