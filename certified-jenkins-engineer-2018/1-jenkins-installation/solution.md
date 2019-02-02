### Jenkins Installation

[Architectural Diagram](/certified-jenkins-engineer-2018/images/lab_diagram_Jenkins_Install.png)

* Jenkins repo is located at wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo 
* The Jenkins key for that repo is located at rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key

1. Install java-1.8.0-openjdk-devel
```bash
$ sudo yum - y install open java-1.8.0-openjdk-devel 
```
```bash
$ java -version
openjdk version "1.8.0_191"
OpenJDK Runtime Environment (build 1.8.0_191-b12)
OpenJDK 64-Bit Server VM (build 25.191-b12, mixed mode)
```

2. Install the repo and key, and then install Jenkins
```bash
$ sudo yum -y install wget
```
```bash
$ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo
```
```bash
$ sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
```
```bash
$ sudo yum -y install jenkins
```
```bash
$ sudo systemctl enable jenkins
jenkins.service is not a native service, redirecting to /sbin/chkconfig.
Executing /sbin/chkconfig jenkins on
```
```bash
$ sudo systemctl start jenkins
```
```bash
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
[initial admin password]
```
```bash
# 1. Access the Getting Started page at http://[server public IP address]:8080
# 2. Copy-paste the initial admin password into the Administrator password textfield and submit.
# 3. Select the Install suggested plugins.
# 4. Create first admin user.
# 5. Click on the Save and finish to complete conguration.
```
[Suggested Plugins](/certified-jenkins-engineer-2018/images/1-suggested-plugins-install.bmp?raw=true)
