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
