### Create a Dockerized Basic Web Server

1. List the base images on the system. Choose a base image for Ubuntu and create a container from that image. This container should be named "basic_web" and should be interactive, attached to the current console and run the bash prompt.
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              7042885a156a        2 weeks ago         109MB
ubuntu              latest              1d9c17228a9e        2 weeks ago         86.7MB
centos              latest              1e1148e4cc2c        6 weeks ago         202MB
```
```bash
$ docker run -it --name="basic_web" ubuntu:latest /bin/bash
root@f53fe3d2ce20:/# 
```

2. Once you are logged into the container at the prompt, install all updates. After updates are installed, install the Apache Web Server and verify that it is listening on Port 80.
```bash
root@f53fe3d2ce20:/# apt-get update && apt-get upgrade && apt-get install apache2
```
```bash
root@f53fe3d2ce20:/# apt-get install telnet
```
```bash
root@f53fe3d2ce20:/# telnet localhost 80
Trying 127.0.0.1...
Trying ::1...
telnet: Unable to connect to remote host: Cannot assign requested address
```
```bash
root@f53fe3d2ce20:/# service apache2 start
 * Starting Apache httpd web server apache2                                   AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
 * 
```
```bash
root@f53fe3d2ce20:/# telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
hello
HTTP/1.1 400 Bad Request
Date: Fri, 18 Jan 2019 02:00:29 GMT
Server: Apache/2.4.29 (Ubuntu)
Content-Length: 302
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.29 (Ubuntu) Server at 172.17.0.2 Port 80</address>
</body></html>
Connection closed by foreign host.
```

3. Using the root account profile file in the root home directory, add the command to start the web server whenever a bash session is started. 
```bash
# Add the line "service apache2 start" to the /root/.bashrc file at the very END
root@f53fe3d2ce20:~# vi .bashrc
```

4. Stop the container. Once stopped, commit the container as a base image called "ubuntu:baseweb".
```bash
$ docker commit basic_web ubuntu:baseweb
sha256:2c9ad6de32899f6b9e8b0db096b6c162ad6b16af1190df233874098cd64c6cd6
```
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              baseweb             2c9ad6de3289        6 seconds ago       263MB
nginx               latest              7042885a156a        2 weeks ago         109MB
ubuntu              latest              1d9c17228a9e        2 weeks ago         86.7MB
centos              latest              1e1148e4cc2c        6 weeks ago         202MB
```

5. Create a container based on the new "ubuntu:baseweb" image called "test_container". It should run interactively, attached to the console and starting a bash prompt. Once logged into the container, verify that the Apache service is running and port 80 is listening. Exit the container.
```bash
$ docker run -it --name="test_container" ubuntu:baseweb /bin/bash
 * Starting Apache httpd web server apache2                                   AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
 * 
root@c7a5b91571b8:/# 
```
```bash
root@c7a5b91571b8:/# telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
hello
HTTP/1.1 400 Bad Request
Date: Fri, 18 Jan 2019 02:10:12 GMT
Server: Apache/2.4.29 (Ubuntu)
Content-Length: 302
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.29 (Ubuntu) Server at 172.17.0.2 Port 80</address>
</body></html>
Connection closed by foreign host.
```
