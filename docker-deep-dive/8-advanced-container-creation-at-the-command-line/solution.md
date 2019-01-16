### Advanced Container Creation at the Command Line

1. Using the Docker base image for Ubuntu, create a container with the following characteristics:

  - Interactive

  - Attached to Terminal

  - Using Google Public DNS

  - Named 'mycontainer1'
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              7042885a156a        2 weeks ago         109MB
centos              latest              1e1148e4cc2c        5 weeks ago         202MB
```
```bash
$ docker run -it --dns=8.8.8.8 --name="mycontainer1" docker.io/ubuntu:latest /bin/bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
84ed7d2f608f: Pull complete 
be2bf1c4a48d: Pull complete 
a5bdc6303093: Pull complete 
e9055237d68d: Pull complete 
Digest: sha256:868fd30a0e47b8d8ac485df174795b5e2fe8a6c8f056cc707b232d65b8a1ab68
Status: Downloaded newer image for ubuntu:latest
root@daa1d5cb3e1e:/# 
```
```bash
root@daa1d5cb3e1e:/# cat /etc/resolv.conf
search mylabserver.com
nameserver 8.8.8.8
```

2. Exit the container from Step #1. Using the Docker base image for Ubuntu, create a container with the following characteristics:

  - Interactive

  - Attached to Terminal 

  - Using Google Public DNS

  - Using Domain Search "mydomain.local"

  - Named 'mycontainer2'
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                          PORTS               NAMES
daa1d5cb3e1e        ubuntu:latest       "/bin/bash"         5 minutes ago       Exited (0) About a minute ago                       mycontainer1
```
```bash
$ docker run -it --dns=8.8.8.8 --dns-search="mydomain.local" --name="mycontainer2" docker.io/ubuntu:latest /bin/bash
root@036e85410d24:/# 
```
```bash
root@036e85410d24:/# cat /etc/resolv.conf
search mydomain.local
nameserver 8.8.8.8
```

3. Exit the container from Step #2. Using the Docker base image for Ubuntu, create a container with the following characteristics:

  - Interactive

  - Attached to Terminal 

  - Using Google Public DNS

  - Using Domain Search "mydomain.local"

  - Create a mount called '/local_vol'

  - Create a mount called '/remote_vol' that mounts the file system in /home/user

  - Named 'mycontainer3'
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                     PORTS               NAMES
036e85410d24        ubuntu:latest       "/bin/bash"         About a minute ago   Exited (0) 3 seconds ago                       mycontainer2
daa1d5cb3e1e        ubuntu:latest       "/bin/bash"         8 minutes ago        Exited (0) 5 minutes ago                       mycontainer1
```
```bash
$ docker run -it --dns=8.8.8.8 --dns-search="mydomain.local" --name="mycontainer3" -v /local_vol -v /home/[user]:/remote_vol docker.io/ubuntu:latest /bin/bash
root@b4a99af17f3f:/#
```
```bash
root@b4a99af17f3f:/# df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          20G  3.0G   17G  16% /
tmpfs            64M     0   64M   0% /dev
tmpfs           496M     0  496M   0% /sys/fs/cgroup
/dev/xvda1       20G  3.0G   17G  16% /local_vol
shm              64M     0   64M   0% /dev/shm
tmpfs           496M     0  496M   0% /proc/acpi
tmpfs           496M     0  496M   0% /proc/scsi
tmpfs           496M     0  496M   0% /sys/firmware
```
```bash
root@b4a99af17f3f:/# cat /etc/resolv.conf
search mydomain.local
nameserver 8.8.8.8
```
```bash
root@b4a99af17f3f:/# cd /local_vol
```
```bash
root@b4a99af17f3f:/local_vol# cd /remote_vol
```
```bash
root@b4a99af17f3f:/remote_vol#
```

4. Exit the container from Step #3. List all the containers. List all characteristics inspected from 'mycontainer2' and then remove and verify removal of all containers.
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
3efe4092467b        ubuntu:latest       "/bin/bash"         2 minutes ago       Exited (0) 9 seconds ago                        mycontainer3
036e85410d24        ubuntu:latest       "/bin/bash"         14 minutes ago      Exited (0) 12 minutes ago                       mycontainer2
daa1d5cb3e1e        ubuntu:latest       "/bin/bash"         20 minutes ago      Exited (0) 17 minutes ago                       mycontainer1
```
```bash
$ docker inspect mycontainer1
[
    {
        "Id": "daa1d5cb3e1e9317466acd45c51d8034a32cacae8da6184461c88b75827980bb",
        "Created": "2019-01-16T12:31:20.343418922Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2019-01-16T12:31:20.734548285Z",
            "FinishedAt": "2019-01-16T12:34:28.6269347Z"
        },
        "Image": "sha256:1d9c17228a9e80a0a23927f24f3cf17d012cf0bb3eae5e3541a8c6987ab9bd5a",
        "ResolvConfPath": "/var/lib/docker/containers/daa1d5cb3e1e9317466acd45c51d8034a32cacae8da6184461c88b75827980bb/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/daa1d5cb3e1e9317466acd45c51d8034a32cacae8da6184461c88b75827980bb/hostname",
        "HostsPath": "/var/lib/docker/containers/daa1d5cb3e1e9317466acd45c51d8034a32cacae8da6184461c88b75827980bb/hosts",
        "LogPath": "/var/lib/docker/containers/daa1d5cb3e1e9317466acd45c51d8034a32cacae8da6184461c88b75827980bb/daa1d5cb3e1e9317466acd45c51d8034a32cacae8da6184461c88b75827980bb-json.log",
        "Name": "/mycontainer1",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Dns": [
                "8.8.8.8"
            ],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "shareable",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": 0,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/ab683ffe986d5ee94ee0949eff7e9e96b054ca50de9d8056e2c81003252073ff-init/diff:/var/lib/docker/overlay2/821b927833eaf2cbd9cc5dc1c7f40de5fbdce6a6221416e491ab7e19fbbdf592/diff:/var/lib/docker/overlay2/f47e937bda76f2ce82d7860a8408bd6a03fbc58f9bfc10c80ce360ec9cf538b5/diff:/var/lib/docker/overlay2/06d44fa9c50ef5726dd4f174b3d3085d0af36d5fde83da20b2a1e480e1116392/diff:/var/lib/docker/overlay2/d615c5cbfd6123102b3910c6f0637ad4491c5a5fb1a7eae2e710b5b03418b59b/diff",
                "MergedDir": "/var/lib/docker/overlay2/ab683ffe986d5ee94ee0949eff7e9e96b054ca50de9d8056e2c81003252073ff/merged",
                "UpperDir": "/var/lib/docker/overlay2/ab683ffe986d5ee94ee0949eff7e9e96b054ca50de9d8056e2c81003252073ff/diff",
                "WorkDir": "/var/lib/docker/overlay2/ab683ffe986d5ee94ee0949eff7e9e96b054ca50de9d8056e2c81003252073ff/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "daa1d5cb3e1e",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "docker.io/ubuntu:latest",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "b1108ec5b932c1fa52f72a684446f8453ef4eca0828f2291e23bf5e1062cb7ff",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/b1108ec5b932",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "fa65b331cf6dc3bf89868c0c9d3b0739afa9201669c1a07e2947db933f9daeeb",
                    "EndpointID": "",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "",
                    "DriverOpts": null
                }
            }
        }
    }
]
```
```bash
$ docker rm `docker ps -a -q`3efe4092467b
036e85410d24
daa1d5cb3e1e
```
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
