# Docker Images
Docker containers are executed based in existing images which are stored in private or public registries. </br>
Private registries/repositories require users to authenticate before pulling images. Public images can be accessed by anyone. </br>
By default, Docker search for images in https://hub.docker.com. </br>

search for an image named `hello-world` in the default public registry

    docker search hello-world

list local images available from the local registry

    docker images

download an image from a public repository

    docker pull hello-world


### Docker Public Registry

login against the `hub.docker.com` registry

    docker login --username=<username>

general form in order to push an image to the repository

    docker push <username>/<iamge>:<version>



