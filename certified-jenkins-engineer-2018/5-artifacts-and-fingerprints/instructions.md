### Artifacts and Fingerprints

There had been a project added to the development process and this project uses the build result from the M3 webdev build. This means that the index.jsp file needs to be input into the backed tomcat project. This new project also is built against the M3 maven server. You will need to create the webdev project and then make sure that the backend tomcat project recieves the index.jsp file from the webdev build. The tomcat project needs to publish test reports for its builds.

At the end of this process you should have a folder named webdev with a freestyle project inside named index. You should also have a folder named backend with a folder named tomcat. The tomcat folder should have a freestyle project in it named tomcat.

You will need 2 git repositories for this lesson:

1. Webapp project: https://github.com/linuxacademy/content-cje-prebuild.git

2. Backend project: https://github.com/linuxacademy/content-jenkinscert.git

**Objectives**
* Create the webdev folder and the index project:
  * Configure maven on the server and name it M3.
  * Under New Item create a folder named webdev. Inside the webdev folder make a freestyle project named index.
  * Configure the project using the git repo in the instructions and ensure that the M3 Maven server is configured. 
  * Run the shell command bin/makeindex and then archive the index.jsp file.
* Install the "Copy Artifact" plugin:
  * Navigate to Manage Jenkins > Manage Plugins.
  * Select available from the tabs at the top.
  * Search for Copy Artifact plugin.
  * Click install, select Restart Jenkins.
  * Wait for Jenkins to restart, you may need to refresh and log back in as student.
* Create and build the tomcat project:
  * Inside the backend > tomcat folder create a freestyle project named tomcat.
  * The first build step should be copy the artifact from the webdev/index job to src/main/webapp in the tomcat job.
  * Then using the M3 maven server run clean package.
  * Create a post build step that publshed junit tests from the target/surefire-reports directory.
  * Run the build and confirm that the tests are published.
