# Docker Architecture

### Docker architecture
The docker daemon and the client can run in the same system or in different systems.
how to communicate with the docker daemon? through the REST API
- unix socket
- network request

### docker daemon
the Docker daemon (dockerd) listen for API requests from clients and manage Docker objects such as images, containers, networks and volumes.

### docker client
the Docker client (docker) communicate with the `daemon` executing requests against the REST API

### docker registry
the docker `registry` is the Docker repository for Docker images

### docker objects
docker objects are the different elements used in order to build, transport and deploy an application through `images`, `containers`, `networks` and `volumes` among others.

### docker images
an `image` is a read only file (several files in fact) with instructions that act as a template for creating Docker containers

### docker containers 
containers are running instances of images, which can be created, started, stopped, moved and removed through the Docker client or the direct interaction with Docker API
