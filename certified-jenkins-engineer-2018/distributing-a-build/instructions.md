### Distibuting a Build 

It has been determined that the resources that are being used for the maven build from M3 need to be reduced and that it would be better if the project was built on more robust hardware, this means that you will need to take the build and make it a distributed build using the provided slave node. This node is not configured and must be setup to perform the build. The freestyle project should be configured to ensure that the build is only run on slave1. The shell bin/makeindex should be run and the index.jsp needs to be archived. Remember that the Jenkins user will need to be added to the slave, keyed to the slave instance and given sudo nopasswd access. The freestyle project name must be mavenproject.

1. The git repo used in this lab is https://github.com/linuxacademy/content-cje-prebuild.git 
2. The shell command that produces the artifact is bin/makeindex Remember to configure the jenkins user access as well as configure the node.

**Objectives**
* Configure the slave machine for use with the Jenkins master. 
* Run the maven build on the remote agent.
