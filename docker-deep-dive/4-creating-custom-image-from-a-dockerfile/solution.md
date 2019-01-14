### Creating Custom Image from a Dockerfile

Reference: [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

1. Create a directory called 'custom' and change to it. In this directory, create an empty file called "Dockerfile". 
```bash
$ mkdir custom
```
```bash
$ cd custom
```
```bash
/custom$ touch Dockerfile 
```

2. Edit the "Dockerfile" created in Step #1 above. This configuration file should be written to perform the following actions:
* Use the base Centos 6 Latest version image from the public repository
* Identify you and your email address as the author and maintainer of this image
* Update the base OS after initial import of the image
* Install the Open-SSH Server
* Install Apache Web Server
* Expose ports 22 and 80 to support the services installed
```bash
/custom$ vi Dockerfile 
```
```bash
# Dockerfile that modifies centos:centos6 to update, include Apache Web
# Server and OpenSSH Server, exposing the appropriate ports
FROM centos:centos6
MAINTAINER User Name <username@domain.com>

# Update the server OS
RUN yum -y upgrade

# Install Apache Web Server
RUN yum -y install httpd

# Install OpenSSH-Server
RUN yum -y install openssh-server

# Expose the SSH and Web Ports for attachment
EXPOSE 22 80
```

3. Build the custom image from the 'Dockerfile' as created above. Name/tag this new image as "mycustomimg/withservices:v1". Once the image is built, verify the image appears in your list.
```bash
/custom$ docker build -t mycustomimg/withservices:v1 .
```
```bash
/custom$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
mycustomimg/withservices   v1                  d703f8ed6b0b        11 seconds ago      421MB
```
