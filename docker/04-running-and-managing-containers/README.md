# Running and Managing containers

### checking docker version
    docker version

### docker `commands` and `help`
getting help from docker

    docker help

getting help for an specific docker command

    docker conatainer help

### docker run
running an `echo` command inside a container from an linux alpine image

    docker container run alpine echo "Hola amigos!"

running a `ping` command inside a container from a linux centos image

    docker container run centos ping -c 5 yahoo.com

### running a container in daemon / detached mode
this bash code exec a `wget` command against a trivia public api that returns random data
``` bash
while :
do
 wget -qO- http://jservice.io/api/random | jq .[0].question
 sleep 2
done
```

lets run the wget command against the trivia public api from a docker container running in daemon / detached mode

    docker container run -d -it --name question ubuntu bash -c "apt update; apt install -y wget jq; while :; do  wget -qO- http://jservice.io/api/random | jq .[0].question; sleep 2; done"

### docker list processes
list docker running containers

    docker container ls

alias for list docker running containers
    docker ps

list docker running containers and only print the container id

    docker container ls -q

list docker all docker containers

    docker ps -a

list docker docker container `id` filtered by `name`

    docker ps -f "name=question" -q

### docker stop
stop a running container named `question`

    docker container stop question

### docker start
restart an stopped container named `question`

    docker container start question

### removing containers
general form to remove a docker container by `id` or by `name`

    docker rm <id | name>

forcing to remove a running container by `name`

    docker rm -f question

remove all running docker containers

    docker container rm -f $(docker container ls -q)

remove all docker containers (included the exited containers)

    docker container rm -f $(docker ps -a -q)

remove all docker containers in `exited` status

    docker ps --no-trunc -aqf "status=exited"| xargs docker rm

### inspect a docker container
general form in order to view the information related to a running container

    docker container inspect <id | name>

view the state information related to a running container named `question`

    docker container inspect -f "{{json .State}}" question | jq '.Status'

### exec a command inside a container
general form in order to exec a command inside a running container

    docker container exec -i -t <id | name> <command>

exec a `bash` prompt in a running container named `question`

    docker container exec -i -t question /bin/sh

### copy files into running containers
run a linux nginx container and name it as `nginx`, mapping the port 80 from the host machine to the port 80 on the container

    docker container run --name nginx -p 80:80 -d nginx:latest

create an `index.html` file and copy it into the running container under the `/usr/share/nginx/html/` directory, which is the default path for the web service

    echo 'hola amigos!' > index.html
    docker container cp index.html nginx:/usr/share/nginx/html/index.html

running an http request against the mapped port on the `host` machine for the content of the web server, we should receive a result like this

    curl http://localhost:80
    hola amigos!

extracting files from a running container 

    docker container cp nginx:/usr/share/nginx/html/index.html extracted-index.html  

### attach to a running container
attach to a running container named `question`

    docker container attach question

### mapping ports
map the port 80 inside a running container to our host at port 8080

    docker run -d --name nginx -p 8080:80 nginx:alpine

interact with process running inside of the docker container through the port 8080 in our host machine

    curl -4 localhost:8080

### viewing container logs
access the logs of a running container named `question`

    docker container logs question

access the last 5 lines of log of a running container named `question`

    docker container logs --tail 5 question

follow the log of a running container named `question`

    docker container logs --follow question

### checking for docker resource consumption
check for resource consumption

    docker stats --all

general form to check resource consumption by `id` or `name`

    docker stats <id | name>

check for specific columns like `cpu`

    docker stats --format "{{.Container}}: {{.CPUPerc}}"

one liner that check for resource consumption grouped by `id`

    docker ps -q | xargs  docker stats --no-stream
