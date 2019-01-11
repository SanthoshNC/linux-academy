### Installation and Image Setup

1. Update your system as appropriate for the distribution you are using, e.g. Ubuntu 16. Use the instructions on the Docker site to add the DOCKER repository for installing the latest copy of Docker for your distribution and version. 

```bash
$ sudo apt-get update
```
```bash
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```
```bash
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```bash
$ sudo apt-key fingerprint 0EBFCD88
pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```
```bash
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

2. Using the appropriate package management commands, install the 'docker' package. Once installed, enable the service so that it starts upon reboot. Additionally, start the 'docker' service and verify it is running.
```bash
$ sudo apt-get update
```
```bash
$ sudo apt-get -y install docker-ce
```
```bash
$ docker --version
Docker version 18.09.1, build 4c52b90
```
```bash
$ sudo docker container run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```
```bash
$ sudo systemctl enable docker
```
```bash
$ sudo systemctl start docker
```
```bash
$ ps aux | grep docker
root     31263  0.0  8.4 535656 85920 ?        Ssl  03:19   0:00 /usr/bin/dockerd -H fd://
```

3. Enable the non-root users to run 'docker' commands on the system. Create the appropriate group, add the users you want to have access to 'docker' commands, restart the 'docker' service and verify that non-root users can run basic 'docker' commands.
```bash
$ sudo groupadd docker
```
```bash
# Add the [your user name] user, e.g. 'user' to the end of that line (after the :)
vim /etc/group
```
```bash
$ cat /etc/group | grep docker
docker:x:999:user
```
Log out from your current session and log in again.
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        10 days ago         1.84kB
```

4.  Once 'docker' is installed and non-root users can run commands, use the appropriate 'docker' commands and options to download the latest available image in the public repository for Ubuntu. Once downloaded and installed, verify the image appears in the local base image list.
```bash
$ docker pull centos:latest
```
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        10 days ago         1.84kB
centos              latest              1e1148e4cc2c        5 weeks ago         202MB
```

5. Start a container based upon the CentOS base image downloaded in Step #4. When you start the container, start it connected to the current terminal, in interactive mode, starting the bash shell for you to connect to. You may exit the container at that time.

```bash
$ docker run -it docker.io/centos:latest /bin/bash
[root@06f9eb1207d6 /]#
```
```bash
[root@06f9eb1207d6 /]# exit
```
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                      PORTS               NAMES
06f9eb1207d6        centos:latest       "/bin/bash"         About a minute ago   Exited (0) 44 seconds ago                       clever_antonelli
```
