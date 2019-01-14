### Managing Containers

References: 
[docker run](https://docs.docker.com/engine/reference/run/), 
[docker restart](https://docs.docker.com/engine/reference/commandline/restart/), 
[docker stop](https://docs.docker.com/engine/reference/commandline/stop/), 
[docker create](https://docs.docker.com/edge/engine/reference/commandline/create/), 
[docker start](https://docs.docker.com/engine/reference/commandline/start/), 
[docker attach](https://docs.docker.com/engine/reference/commandline/attach/)
1. Create a container from the base image for the latest version of CentOS available (if you do not have an CentOS base image installed locally, pull the latest one down for your local repository). The container should be started in interactive mode attached to the current terminal and running the bash shell. Once running, shut the container down by exiting.
```bash
$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
hello-world                latest              fce289e99eb9        13 days ago         1.84kB
centos                     latest              1e1148e4cc2c        5 weeks ago         202MB
```
```bash
$ docker run -it centos:latest /bin/bash
```
```bash
[root@0844f3cffc68 /]# exit
exit
```

2. Run the appropriate Docker command to get the name of the previously run container. Issue the appropriate command to restart the container that you obtained the name of. Do NOT create a new container, restart the one we just used.
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS                  NAMES
0844f3cffc68        centos:latest       "/bin/bash"         10 seconds ago      Exited (0) 4 seconds ago                           boring_noyce
```
```bash
$ docker restart boring_noyce
boring_noyce
```
```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
0844f3cffc68        centos:latest       "/bin/bash"         3 minutes ago       Up 40 seconds                           boring_noyce
```

3. Stop the container. Remove that container from the system completely using the appropriate command.
```bash
$ docker stop boring_noyce
boring_noyce
```
```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                            PORTS                  NAMES
0844f3cffc68        centos:latest       "/bin/bash"         6 minutes ago       Exited (137) About a minute ago                          boring_noyce
4b9dcf55aeae        centos:centos6      "/bin/bash"         13 hours ago        Exited (255) 10 hours ago         0.0.0.0:8022->22/tcp   test_ssh
```
```bash
$ docker rm boring_noyce
boring_noyce
```
```bash
$ docker ps -a
4b9dcf55aeae        centos:centos6      "/bin/bash"         13 hours ago        Exited (255) 10 hours ago         0.0.0.0:8022->22/tcp   test_ssh
```

4. Create (not run) a container called "my_container", create it with parameters that will allow it to run interactively and attached to the local console running the bash shell. Verify that the container is not running.
```bash
$ docker create -it --name="my_container" centos:latest /bin/bash
29dcd2721c3ab089946ab73be570604b17bf87ffa0b3ab36e5bd1b6c0055883d
```
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS                  NAMES
29dcd2721c3a        centos:latest       "/bin/bash"         37 seconds ago      Created                                            my_container
4b9dcf55aeae        centos:centos6      "/bin/bash"         13 hours ago        Exited (255) 10 hours ago   0.0.0.0:8022->22/tcp   test_ssh
```

5. Start the container and again, verify the container is running. Run the appropriate command to attach your session to the running container so you are logged into the shell.
```bash
$ docker start my_container
my_container
```
```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
29dcd2721c3a        centos:latest       "/bin/bash"         2 minutes ago       Up 34 seconds                           my_container
```
```bash
$ docker attach my_container
[root@29dcd2721c3a /]#
```
```bash
[root@29dcd2721c3a /]# exit
exit
```
