### Artifacts and Fingerprints

There had been a project added to the development process and this project uses the build result from the M3 webdev build. This means that the index.jsp file needs to be input into the backed tomcat project. This new project also is built against the M3 maven server. You will need to create the webdev project and then make sure that the backend tomcat project recieves the index.jsp file from the webdev build. The tomcat project needs to publish test reports for its builds.

At the end of this process you should have a folder named webdev with a freestyle project inside named index. You should also have a folder named backend with a folder named tomcat. The tomcat folder should have a freestyle project in it named tomcat.

You will need 2 git repositories for this lesson:

1. Webapp project: https://github.com/linuxacademy/content-cje-prebuild.git

2. Backend project: https://github.com/linuxacademy/content-jenkinscert.git

**Objectives**
* Create the webdev folder and the index project.
* Install the "copy artifact" plugin
* Create and build the tomcat project
