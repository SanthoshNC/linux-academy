### Base Image Maintenance and Cleanup

1. List all currently install Docker images. If you do not have at least three Docker base images at this point, please pull down other Docker images and/or follow the other exercises in this tutorial.
```bash
$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
mycustomimg/withservices   v1                  d703f8ed6b0b        43 hours ago        421MB
newcentos                  withapache          cc6399740517        2 days ago          306MB
hello-world                latest              fce289e99eb9        2 weeks ago         1.84kB
nginx                      latest              7042885a156a        2 weeks ago         109MB
centos                     centos6             0cbf37812bff        3 months ago        194MB
```
```bash
$ docker run -itd centos:centos6
1468833c7e8e46125905ed46d9f2032a48d83d8485174ab1bee5b9250a432c28
```

2. Execute the command to remove a base image that you have previously created a container from and note the resulting message.
```bash
$ docker rmi centos:centos6
Error response from daemon: conflict: unable to remove repository reference "centos:centos6" (must force) - container 4b9dcf55aeae is using its referenced image 0cbf37812bff
```

3. Run the appropriate command to remove the container that Step #2 indicated is preventing the deletion of that base image.
```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
1468833c7e8e        centos:centos6      "/bin/bash"         3 minutes ago       Up 3 minutes                            xenodochial_mcnulty
```
```bash
$ docker stop 1468833c7e8e
1468833c7e8e
```
```bash
$ docker rm 1468833c7e8e
1468833c7e8e
```

4. List all previously run containers and remove all of them one at a time. Verify that the command to list stopped containers shows nothing before continuing.
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS                   NAMES
3e9167755f34        0cbf37812bff        "/bin/bash"              8 minutes ago       Exited (0) 7 minutes ago                              jolly_goodall
ee95b513bc36        nginx:latest        "nginx -g 'daemon of…"   19 hours ago        Exited (255) 14 minutes ago   0.0.0.0:32768->80/tcp   sleepy_ganguly
f56c826cbb15        nginx:latest        "nginx -g 'daemon of…"   19 hours ago        Exited (0) 19 hours ago                               hardcore_dijkstra
8dd243619575        centos:centos6      "/bin/bash"              24 hours ago        Exited (0) 24 hours ago                               remote_vol
c0d66b66b781        centos:centos6      "/bin/bash"              24 hours ago        Exited (130) 24 hours ago                             local_vol
29dcd2721c3a        centos:latest       "/bin/bash"              33 hours ago        Exited (0) 33 hours ago                               my_container
4b9dcf55aeae        centos:centos6      "/bin/bash"              47 hours ago        Exited (255) 43 hours ago     0.0.0.0:8022->22/tcp    test_ssh
b0f429a086ea        centos:latest       "/bin/bash"              2 days ago          Exited (0) 2 days ago                                 wizardly_joliot
80f41175ca59        centos:centos6      "/bin/bash"              2 days ago          Created                                               serene_noyce
```
```bash
```
```bash
```

5. Rerun the command executed in Step #2 and then list the base images on your system.
```bash
```
```bash
```
```bash
```
