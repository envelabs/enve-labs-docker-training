# Docker Images
Container images are files that works as read only templates from which containers are created. These images are composed of many layers, where the first layer in the image is called the base layer. Each layer of the image is a well defined instruction related to a package installation or an specific setup required by the application in order to run.

There are three methods in order to create an image. The first one is by interactively building a container which contains all the changes required and then saving those changes into a new image. The second, building an image based in a manifest usually known as `Dockerfile`. And the third one is to importing the image into the system from a tarball, which is an specific file type that collects and group several files.


### Docker Image Search
search for an image named `hello-world` in the default public registry

    docker search hello-world

list local images available from the local registry

    docker image ls

download an image from a public repository

    docker image pull hello-world

search by specific tags against docker hub api v1

    wget -q https://registry.hub.docker.com/v3/repositories/debian/tags -O - | jq -r '.[].name'

search by specific tags against docker hub api v2

    curl -s 'https://registry.hub.docker.com/v2/repositories/library/debian/tags/' | jq -r '."results"[]["name"]'

### Creating an image from a running container
running a container named `enve-alpine-test` and get a shell inside of the running container

    docker container run -it --name enve-alpine-test alpine:3.10 /bin/sh

install the `ping` utility in the running container

    apk update && apk add iputils


execute a ping command against `yahoo.com` from the running container

    ping -c 5 yahoo.com


exit from the container

    exit


list all the containers (including those in the `exited` status)

    docker ps -a


identify the differences between the container named `enve-alpine-test` and its original image with the `diff` subcommand  

    docker container diff enve-alpine-test


commit (save) the changes made in the container named `enve-alpine-test` and create a new image named `enve-alpine-ping`

    docker container commit enve-alpine-test enve-alpine-ping

check for the new `enve-alpine-ping` image

    docker image ls

review the history of the `enve-alpine-ping` image

    docker image history enve-alpine-ping


### Docker Image creation from a Dockerfile
image build from a Dockerfile in order to install the ping command and exec it against `yahoo.com` (`dockerfile-enve-ubuntu-ping` file in the directory should be copied to `Dockerfile`, which is the default file used by the `docker build` process)

    cp dockerfile-enve-ubuntu-ping Dockerfile

    docker image build --tag enve-ubuntu-ping .


another method is to pass the content of the dockerfile for stdin

    cat dockerfile-enve-ubuntu-ping | docker build -t enve-ubuntu-ping -


also it is possible to pass the name of the dockerfile as param

    docker image build --tag enve-ubuntu-ping --file dockerfile-enve-ubuntu-ping .

run a container from the `enve-ubuntu-ping` image in order to test the ping command

    docker container run --rm -it enve-ubuntu-ping


image build from a Dockerfile in order to install nginx server

    docker image build --tag enve-ubuntu-nginx --file dockerfile-enve-ubuntu-nginx .


run a container from the `enve-ubuntu-nginx` image in order to test the nginx server

    docker container run --rm -it --name enve-ubuntu-nginx enve-ubuntu-nginx

### Docker creation from a running container into a `tarball` file
image save into a tarball file

    docker image save -o ./enve-ubuntu-nginx-img.tar enve-ubuntu-nginx

image load from the `tarball` file into the local registry

    docker image load -i /enve-ubuntu-nginx-img.tar

### Docker image remove
general form in order to remove an image from the local repository

    docker image rm <image_id>

remove unused docker Images

    docker image prune

### Docker Public Registry
Docker containers are executed based in existing images which are stored in private or public registries. Private registries or repositories require users to authenticate before pulling images. Public images can be accessed by anyone. </br>
By default, Docker search for images in https://hub.docker.com. </br>

general form to login against the `hub.docker.com` registry in order to get access to private repos associated with your account

    docker login --username=<username>

general form in order to push an image to the registry

    docker push <username>/<iamge>:<version>
