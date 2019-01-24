### Distibuting a Build 

It has been determined that the resources that are being used for the maven build from M3 need to be reduced and that it would be better if the project was built on more robust hardware, this means that you will need to take the build and make it a distributed build using the provided slave node. This node is not configured and must be setup to perform the build. The freestyle project should be configured to ensure that the build is only run on slave1. The shell bin/makeindex should be run and the index.jsp needs to be archived. Remember that the Jenkins user will need to be added to the slave, keyed to the slave instance and given sudo nopasswd access. The freestyle project name must be mavenproject.

1. The git repo used in this lab is https://github.com/linuxacademy/content-cje-prebuild.git 
2. The shell command that produces the artifact is bin/makeindex Remember to configure the jenkins user access as well as configure the node.

**Objectives**
* Configure the slave machine for use with the Jenkins master. 

##### Master
```bash
$ sudo su
```
```bash
# cat /etc/passwd | grep jenkins
jenkins:x:996:993:Jenkins Automation Server:/var/lib/jenkins:/bin/false
```
```bash
### replace /bin/false with /bin/bash
$ vim /etc/passwd
```
```bash
# cat /etc/passwd | grep jenkins
jenkins:x:996:993:Jenkins Automation Server:/var/lib/jenkins:/bin/bash
```
```bash
# passwd jenkins
Changing password for user jenkins.
New password: 
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: 
passwd: all authentication tokens updated successfully.
```
```bash
# su jenkins
bash-4.2$ whomi
bash: whomi: command not found
bash-4.2$ whoami
jenkins
bash-4.2$ pwd
/home/cloud_user
bash-4.2$ cd 
bash-4.2$ pwd
/var/lib/jenkins
bash-4.2$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/var/lib/jenkins/.ssh/id_rsa): 
Created directory '/var/lib/jenkins/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /var/lib/jenkins/.ssh/id_rsa.
Your public key has been saved in /var/lib/jenkins/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:R9Meb0wXoY12VF7nArkRUyvjiBpw6p7fnObkZ+pUoA0 jenkins@jenkins
The key's randomart image is:
+---[RSA 2048]----+
|            ++.+*|
|           .oo=++|
|    . E . o =*+o+|
|     + + + =oB.o |
|    . o S + o +  |
|   .   o o   .   |
|    . . o        |
|   . . *..o      |
|    o..+O+       |
+----[SHA256]-----+
bash-4.2$ ssh cloud_user@[slave IP address]
```

##### Slave
```bash
$ sudo su
```
```bash
# useradd jenkins
```
```bash
# passwd jenkins
Changing password for user jenkins.
New password: 
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: 
passwd: all authentication tokens updated successfully.
```
```bash
### Add 'jenkins ALL=(ALL)  NOPASSWD: ALL' after 'root    ALL=(ALL)       ALL'
# visudo
```
```bash
# exit
```
```bash
$ exit
logout
Connection to [Slave IP address] closed.
```
##### Master
```bash
$ ssh-copy-id jenkins@[slave IP address]
/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/var/lib/jenkins/.ssh/id_rsa.pub"
/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
jenkins@184.72.86.53's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'jenkins@[slave IP address]'"
and check to make sure that only the key(s) you wanted were added.
```
```bash
bash-4.2$ cat ./.ssh/id_rsa
-----BEGIN RSA PRIVATE KEY-----
[RSA private key content]
-----END RSA PRIVATE KEY-----
bash-4.2$
```
##### Jenkins UI
In Manage Jenkins/Manage Nodes add new node named **slave1**: [slave node config](), [slave node credentials config]() 

* Run the maven build on the remote agent.
