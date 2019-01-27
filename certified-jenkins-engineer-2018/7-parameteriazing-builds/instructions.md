### Parameterizing Builds

The web dev team has indicated that they have made a recent change to the index project and that this project now needs to have a name supplied so that the build can be customized. This is a maven project from teh M3 server. The name should be provided in string format, and the name should be Steve.

Remember that the webdev project is a maven project and you will need to create the maven server M3

Git repo to use: https://github.com/linuxacademy/content-cje-prebuild.git

**Objectives**
* Create the webdev folder and index freestyle project
  * On the dash board create a new item named webdev make it a folder.
  * Inside of webdev make a freestyle project named index.
* Configure the index project to accept the name Steve
  * In the index project click this build requires parameters.
  * Add a string parameter called name, the value should be Steve.
  * Add the Git repo.
  * Add the Maven server M3.
  * Add the shell command to make the bin/makeindex.
  * Make a post build action to archive the artifact.
  * Check the artifat to ensure that it says "Hello Steve".
