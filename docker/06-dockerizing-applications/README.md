# Dockerizing Applications

Image creation of custom images requires a method in order to avoid errors  produced by the human interaction at execution time. Also, reproducible of the process and scalability should be considered in order to generate a robust build process. Dockerfiles help us to solve this problems, allowing us to build images from a file that act as a `manifest` that contains in a declarative way the instructions required in order to build the image.

### Structure of a Dockerfiles

A Dockerfile is a file composed by several lines, each of one represent an action to be executed during the image process build. Each action is defined by a `keyword` such as `FROM`, `RUN` or `ADD` at the beginning of each line that usually is written in caps, which is not a must.


    FROM <image-base>
    WORKDIR <build-process-dir>
    COPY <src> <dst>
    ADD <src> <dst>
    RUN <cmd>
    EXPOSE <port-to-be-exposed-by-the-container>
    ENTRYPOINT  <default-command-to-be-exec>
    CMD <default-command-to-exec|params-for-entrypoint>

### Building an application
in the current directory there is a `Dockerfile` that we are going to use in order to build a new image which contains a `node` image as a `base image` and then exec a build process for a very simple nodejs app that will expose its functionality in the port 8080.

In order to build the new image we can exec

    docker image build -t enve-nodejs-app:latest .
