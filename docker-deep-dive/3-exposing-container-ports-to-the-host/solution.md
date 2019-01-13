### Exposing Container Ports to the Host

NOTE: The solution below assumes Ubuntu 16 distribution.

References: [docker run](https://docs.docker.com/engine/reference/commandline/run/), [docker attach](https://docs.docker.com/engine/reference/commandline/attach/) 

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
docker run -itd centos:centos6 /bin/bash
```
```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
30a2227d033f        centos:centos6      "/bin/bash"         50 seconds ago      Up 49 seconds                           dazzling_goldberg
```
```bash
$ docker inspect dazzling_goldberg | grep IP
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
```
```bash
$ ping -c 3 172.17.0.2
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.062 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.048 ms
64 bytes from 172.17.0.2: icmp_seq=3 ttl=64 time=0.048 ms

--- 172.17.0.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1998ms
rtt min/avg/max/mdev = 0.048/0.052/0.062/0.010 ms
```
```bash
$ docker attach dazzling_goldberg
[root@30a2227d033f /]#
```

2. Using the appropriate Docker inspection command, find the IP address and name for the running container. Once you have the IP, ping the IP to be sure it is running. Finally, attach to the running container so you are logged into the shell.

3. From within the container, install the Open-SSH server and make sure the service is running. From another terminal, try to log into the container over SSH by IP and note the result.

4. Exit and stop the container. Remove the container from the list of previously run containers once you obtain the name from the appropriate Docker command.

5. Create another container, name this container 'test_ssh'. When creating the container, it should be run in interactive mode and attached to the current terminal running the bash shell. Finally, expose port 22 on the container to port 8022 on the host system. Once logged in, install the Open-SSH server and make sure the service is running. Find the IP address of the container and note it.

6. Install the 'sudo' utility. Add a user called 'test' and set a password for that user. Add the 'test' user to the 'sudoers' file. From another terminal window, attempt to log into the container via SSH as the 'test' user and confirm access.
