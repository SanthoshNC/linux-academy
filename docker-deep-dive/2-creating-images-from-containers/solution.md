### Creating Images from Containers

NOTE: The solution below assumes Ubuntu 16 distribution.

References: [docker run](https://docs.docker.com/engine/reference/commandline/run/) 

1. Using the CentOS 6 base image download, start a container based on that image. Be sure that container starts connected to the current terminal in interactive mode and runs the bash command so you are logged in to the command prompt on the container once it boots.
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        12 days ago         1.84kB
centos              latest              1e1148e4cc2c        5 weeks ago         202MB
```
```bash
# --interactive, -i Keep STDIN open even if not attached
# --tty, -t Allocate a pseudo-TTY
# /bin/bash Provide interactive shell
$ docker run -it centos:centos6 /bin/bash
[root@b0f429a086ea /]#
```

2. Once you are sitting at a command prompt on the running container, execute the update command (installing all updates for the container OS).
```bash
[root@b0f429a086ea /]# yum -y update
```

3. Now that updates are complete, install the Apache Web Server. Once installed, make sure the web server service will start and verify that the container is listening on port 80 (install other software if needed to do so).
```bash
[root@b0f429a086ea /]# yum install httpd
```
```bash
[root@b237d65fd197 /]# yum install telnet
```
```bash
[root@b237d65fd197 /]# service httpd start
Starting httpd: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2 for ServerName
```
```bash
[root@b237d65fd197 /]# telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
```

4. Exit the container. Once the container is stopped, execute the appropriate command to list all stopped containers and locate the name and ID of the container you just exited. Make a note of the name and ID.
```bash
[root@b237d65fd197 /]# exit
```
```bash
$ docker pa -a 
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
caea59ff8906        centos:centos6      "/bin/bash"         4 minutes ago       Exited (1) 7 seconds ago                       thirsty_newton
```

5. Using the name or ID of the container, commit the changes you made within it to a new base image called "newcentos:withapache" and verify that it shows when you list the images on your system.
```bash
$ docker commit caea59ff8906 newcentos:withapache
```
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
newcentos           withapache          cc6399740517        8 seconds ago       306MB
hello-world         latest              fce289e99eb9        12 days ago         1.84kB
centos              latest              1e1148e4cc2c        5 weeks ago         202MB
centos              centos6             0cbf37812bff        3 months ago        194MB
```
