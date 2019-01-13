### Exposing Container Ports to the Host

NOTE: The solution below assumes Ubuntu 16 distribution.

References: [docker run](https://docs.docker.com/engine/reference/commandline/run/) 

1. Create a container from the 'centos:6' base image on your system. This container does not need to be name but should be run in daemon mode, interactive and connected to the current terminal. Finally, it should start the bash shell on start up
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
newcentos           withapache          cc6399740517        About an hour ago   306MB
hello-world         latest              fce289e99eb9        12 days ago         1.84kB
centos              latest              1e1148e4cc2c        5 weeks ago         202MB
centos              centos6             0cbf37812bff        3 months ago        194MB
```
```bash
# --interactive, -i Keep STDIN open even if not attached
# --tty, -t Allocate a pseudo-TTY
# --detach, -d Run container in background and print container ID
# /bin/bash Provide interactive shell
$ docker run -itd centos:centos6 /bin/bash
```
```bash
```
```bash
```
```bash
```
```bash
```

2. Using the appropriate Docker inspection command, find the IP address and name for the running container. Once you have the IP, ping the IP to be sure it is running. Finally, attach to the running container so you are logged into the shell.

3. From within the container, install the Open-SSH server and make sure the service is running. From another terminal, try to log into the container over SSH by IP and note the result.

4. Exit and stop the container. Remove the container from the list of previously run containers once you obtain the name from the appropriate Docker command.

5. Create another container, name this container 'test_ssh'. When creating the container, it should be run in interactive mode and attached to the current terminal running the bash shell. Finally, expose port 22 on the container to port 8022 on the host system. Once logged in, install the Open-SSH server and make sure the service is running. Find the IP address of the container and note it.

6. Install the 'sudo' utility. Add a user called 'test' and set a password for that user. Add the 'test' user to the 'sudoers' file. From another terminal window, attempt to log into the container via SSH as the 'test' user and confirm access.
