### Adding External Content to Containers

1. Create a directory in your 'user' home directory called 'docker'. Within that directory, create another directory called 'mydata'. Within that directory, create a file called 'mydata.txt' containing any text message you want.
```bash
$ mkdir docker
```
```bash
$ cd docker
```
```bash
/docker$ mkdir mydata
```
```bash
/docker$ cd mydata
```
```bash
/docker/mydata$ echo "this is data from the underlying host" >> mydata.txt
```
```bash
/docker/mydata$ cat mydata.txt
this is data from the underlying host
```

2. Create a docker container name 'local_vol' from the 'centos:centos6' image. The container should be created in interactive mode, attached to the current terminal and running the bash shell. This container should contain a volume (or directory) called 'containerdata' so that the system will automatically create the directory/mount when the container starts.
```bash
$ docker run -it --name="local_vol" -v /containerdata centos:centos6 /bin/bash
[root@c0d66b66b781 /]# 
```

3. List the filesystems within the container, specifically looking for the volume/directory that was added to the container during creation.
```bash
[root@c0d66b66b781 /]# df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          20G  3.5G   16G  19% /
tmpfs            64M     0   64M   0% /dev
tmpfs           496M     0  496M   0% /sys/fs/cgroup
/dev/xvda1       20G  3.5G   16G  19% /containerdata
/dev/xvda1       20G  3.5G   16G  19% /etc/resolv.conf
/dev/xvda1       20G  3.5G   16G  19% /etc/hostname
/dev/xvda1       20G  3.5G   16G  19% /etc/hosts
```
```bash
[root@c0d66b66b781 /]# ls -al /containerdata/
total 8
drwxr-xr-x 2 root root 4096 Jan 14 21:22 .
drwxr-xr-x 1 root root 4096 Jan 14 21:22 ..
```

4. Exit the container. This time, create another container called 'remote_vol' with the same container configuration except when creating the volume in the container, link the volume name 'mydata' to the underlying host directory structure created in Step #1.
```bash
$ docker run -it --name="remote_vol" -v /home/user/docker/mydata:/mydata centos:centos6 /bin/bash
[root@8dd243619575 /]# 
```

5. Once the container is started, list the disk mounts and verify the remote (host) volume is mounted. Change to that directory and verify that the text file created in Step #1 appears with the content created.
```bash
[root@8dd243619575 /]# df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          20G  3.5G   16G  19% /
tmpfs            64M     0   64M   0% /dev
tmpfs           496M     0  496M   0% /sys/fs/cgroup
/dev/xvda1       20G  3.5G   16G  19% /mydata
/dev/xvda1       20G  3.5G   16G  19% /etc/resolv.conf
/dev/xvda1       20G  3.5G   16G  19% /etc/hostname
/dev/xvda1       20G  3.5G   16G  19% /etc/hosts
```
```bash
[root@8dd243619575 /]# ls -al /mydata
total 12
drwxrwxr-x 2 1001 1001 4096 Jan 14 21:15 .
drwxr-xr-x 1 root root 4096 Jan 14 21:29 ..
-rw-rw-r-- 1 1001 1001   38 Jan 14 21:15 mydata.txt
```
```bash
[root@8dd243619575 /]# cat /mydata/mydata.txt
this is data from the underlying host
```
