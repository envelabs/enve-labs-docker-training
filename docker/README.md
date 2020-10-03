# Enve Labs Training - Docker
This directory contains a list of commands required to run an application inside a docker container in a virtualized environment.</br>
Please note that this process was successfully tested in macOS and Linux host systems, hopefully this will work also in Windows environments.

### Prerequisites

- VirtualBox (https://www.virtualbox.org) must be installed on your computer.
- Vagrant (https://vagrantup.com) must be installed on your computer.


we going to deploy a linux virtual machine through `Vagrant` with all the required packages in order to run `Docker` inside.  

### Environment creation
deploy the VM with all the required packages

    vagrant up

connect to the VM in order to work with Docker

    vagrant ssh

stop the VM

    vagrant stop


clean up when you're done (this process will destroy de VM and all its content will be lost)

    vagrant destroy
