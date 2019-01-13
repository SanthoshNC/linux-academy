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
```

2. Using the appropriate Docker inspection command, find the IP address and name for the running container. Once you have the IP, ping the IP to be sure it is running. Finally, attach to the running container so you are logged into the shell.
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
3. From within the container, install the Open-SSH server and make sure the service is running. From another terminal, try to log into the container over SSH by IP and note the result.
```bash
[root@f9d9fa5c92df /]# yum install openssh-server
```
```bash
[root@f9d9fa5c92df /]# service sshd start        
Generating SSH2 RSA host key:                           [  OK  ]
Generating SSH1 RSA host key:                           [  OK  ]
Generating SSH2 DSA host key:                           [  OK  ]
Starting sshd:                                          [  OK  ]
```
```bash
$ ssh test@172.17.0.2
ssh: connect to host 172.17.0.2 port 22: Connection refused
```

4. Exit and stop the container. Remove the container from the list of previously run containers once you obtain the name from the appropriate Docker command.
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS               NAMES
f9d9fa5c92df        centos:centos6      "/bin/bash"         26 minutes ago      Exited (255) 7 seconds ago                       stupefied_blackburn
30a2227d033f        centos:centos6      "/bin/bash"         37 minutes ago      Exited (0) 26 minutes ago                        dazzling_goldberg
caea59ff8906        centos:centos6      "/bin/bash"         6 hours ago         Exited (1) 6 hours ago                           thirsty_newton
```
```bash
$ docker rm stupefied_blackburn
```
```bash
$ docker rm dazzling_goldberg
```
```bash
$ docker rm thirsty_newton
```
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
newcentos           withapache          cc6399740517        6 hours ago         306MB
hello-world         latest              fce289e99eb9        12 days ago         1.84kB
centos              latest              1e1148e4cc2c        5 weeks ago         202MB
centos              centos6             0cbf37812bff        3 months ago        194MB
```

5. Create another container, name this container 'test_ssh'. When creating the container, it should be run in interactive mode and attached to the current terminal running the bash shell. Finally, expose port 22 on the container to port 8022 on the host system. Once logged in, install the Open-SSH server and make sure the service is running. Find the IP address of the container and note it.
```bash
# --publish, -p Publish a container’s port(s) to the host
$ docker run -it --name="test_ssh" -p 8022:22 docker.io/centos:centos6 /bin/bash 
[root@4b9dcf55aeae /]#
```
```bash
[root@4b9dcf55aeae /]# yum install -y openssh-server
```
```bash
[root@4b9dcf55aeae /]# service sshd start
Generating SSH2 RSA host key:                           [  OK  ]
Generating SSH1 RSA host key:                           [  OK  ]
Generating SSH2 DSA host key:                           [  OK  ]
Starting sshd:                                          [  OK  ]
```
```bash
[root@4b9dcf55aeae /]# ifconfig
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:15226 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8763 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:30839682 (29.4 MiB)  TX bytes:512928 (500.9 KiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)
```

6. Install the 'sudo' utility. Add a user called 'test' and set a password for that user. Add the 'test' user to the 'sudoers' file. From another terminal window, attempt to log into the container via SSH as the 'test' user and confirm access.
```bash
[root@4b9dcf55aeae /]# yum install sudo
```
```bash
[root@4b9dcf55aeae /]# adduser test
```
```bash
[root@4b9dcf55aeae /]# passwd test
Changing password for user test.
New password: 
Retype new password: 
passwd: all authentication tokens updated successfully.
```
```bash
[root@4b9dcf55aeae /]# usermod -aG wheel test
```
```bash
# Add the following line 'test        ALL=(ALL)      ALL'
[root@4b9dcf55aeae /]$ visudo
```
```bash
[root@4b9dcf55aeae /]# sudo cat /etc/sudoers | grep test
test    ALL=(ALL)      ALL
```
```bash
$ ssh test@172.17.0.2
The authenticity of host '172.17.0.2 (172.17.0.2)' can't be established.
RSA key fingerprint is SHA256:JIlMvPEzC0zCMRrIGogn7baLw6IJzPoaK6fLJVGZhkU.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '172.17.0.2' (RSA) to the list of known hosts.
test@172.17.0.2's password: 
[test@4b9dcf55aeae ~]$
```
```bash
[test@4b9dcf55aeae ~]$ sudo ls -la /root
[sudo] password for test: 
total 44
dr-xr-x--- 2 root root 4096 Oct  6 20:19 .
drwxr-xr-x 1 root root 4096 Jan 13 23:13 ..
-rw------- 1 root root 2687 Oct  6 20:19 anaconda-ks.cfg
-rw-r--r-- 1 root root   18 May 20  2009 .bash_logout
-rw-r--r-- 1 root root  176 May 20  2009 .bash_profile
-rw-r--r-- 1 root root  176 Sep 23  2004 .bashrc
-rw-r--r-- 1 root root  100 Sep 23  2004 .cshrc
-rw-r--r-- 1 root root 7289 Oct  6 20:19 install.log
-rw-r--r-- 1 root root 1680 Oct  6 20:18 install.log.syslog
-rw-r--r-- 1 root root  129 Dec  3  2004 .tcshrc
```
