# Docker Images
Container images are templates from which containers are created. These images are composed of many layers, where the first layer in the image is called the base layer. Each layer of the image is a well defined action related to a package installation or an specific setup required by the application in order to run.


search for an image named `hello-world` in the default public registry

    docker search hello-world

list local images available from the local registry

    docker images

download an image from a public repository

    docker pull hello-world

search by specific tags against docker hub api v1

    wget -q https://registry.hub.docker.com/v3/repositories/debian/tags -O - | jq -r '.[].name'

search by specific tags against docker hub api v2

    curl -s 'https://registry.hub.docker.com/v2/repositories/library/debian/tags/' | jq -r '."results"[]["name"]'

### Creating an image from a running container
running a container named `enve-alpine-test` and get a shell inside

    docker container run -it --name enve-alpine-test alpine:3.10 /bin/sh

install ping utils in the running container

    apk update && apk add iputils


ping `yahoo.com` from the container

    ping -c 5 yahoo.com


exit from the container

    exit


list all the containers (including those in the `exited` status)

    docker ps -a


diff container named `enve-alpine-test`

    docker container diff enve-alpine-test


commit (save) the changes made in the container named `enve-alpine-test` and create a new image named `enve-alpine-ping`

    docker container commit enve-alpine-test enve-alpine-ping

check for the new `enve-alpine-ping` image

    docker image ls

review the history of the `history enve-alpine-ping` image

    docker image history enve-alpine-ping


### Docker Image creation from a Dockerfile
image build from a Dockerfile in order to install the ping command and exec it against `yahoo.com` (`dockerfile-enve-ping` file in the directory should be copied to `Dockerfile`, which is the default file used by the `docker build` process)

    docker image build -t enve-alpine-ping-img .


run a container from the `enve-alpine-ping-img` image in order to test the ping command

    docker container run --rm -it enve-alpine-ping-img


image build from a Dockerfile in order to install a nginx server and and expose it in the port 80 (`dockerfile-enve-nginx` file in the directory should be copied to `Dockerfile`, which is the default file used by the `docker build` process)

        docker image build -t enve-ubuntu-nginx-img .


run a container from the `enve-ubuntu-nginx-img` image in order to test the nginx server

    docker container run --rm -it --name enve-ubuntu-nginx-v2 enve-ubuntu-nginx-img

### Docker creation from a running container into a `tarball` file
image save into a tarball file

    docker image save -o ./enve-ubuntu-nginx-img-v2.tar enve-ubuntu-nginx-v2

image load from the `tarball` file into the local registry

    docker image load -i /enve-ubuntu-nginx-img-v2.tar


### Docker Public Registry
Docker containers are executed based in existing images which are stored in private or public registries. Private registries or repositories require users to authenticate before pulling images. Public images can be accessed by anyone. </br>
By default, Docker search for images in https://hub.docker.com. </br>

general form to login against the `hub.docker.com` registry in order to get access to private repos associated with your account

    docker login --username=<username>

general form in order to push an image to the registry

    docker push <username>/<iamge>:<version>
