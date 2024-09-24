# Summary

## Purpose
I created this repository to keep hold of playbooks I create as I go through learning and improving my Ansible skills.For those interested in following along and trying out any playbooks I create, I will explain my lab environment.

## Setup

### Machine Being Used?
I am using a Windows 10 machine. I have WSL (Windows Subsystem for Linux) install so that I can operate as if I was using a Linux machine without the need of a virtual machine or dual-boot setup. I also have Docker Desktop installed on my machine as well for container usage.

### What Are Playbooks Being Ran Against?
As mentioned before, I have Docker Desktop set up on my machine. I have five containers created for the purpose of using them as targets for my playbooks. Virtual Machines can be used instead of containers, but for convenience sake, I will only be using containers as targets (5). There is a docker file in this repository that is used to create the containers. You must first build the image for the container using the docker file using the following steps:

Generate your id rsa keys and place them in the docker/ansible-containers directory when it prompts for a location for the keys:
```
ssh-keygen -t rsa -b 4096
location: <path-to-Ansible-directory>/docker/ansible-containers
```
Build your image:
```
cd docker/ansible-containers
docker build -t <name your image> .
```

Create your container:

```
docker run -d --name <name your container> -p <give it an available port>:22 <image name>
```

Validate you can remote login to the container:

```
ssh root@localhost -p <port you assigned>
```