### Build Triggers

All of the projects that have been created so far have been isolated and it is now time to link the jobs, create the index project in webdev, the tomcat project in backend, remeber that the index project should take a name argument and that the artifact of the index project needs to be sent to the tomcat project. The tomcat project should watch the index project to know when to build.

These projects use the maven M3 server, the index project needs to run bin/makeindex to create the index.jsp Tomcat needs to pull from index. The archive path in tomcat is src/main/webapp/index.jsp

GitHub repos to use:
* index job - https://github.com/linuxacademy/content-cje-prebuild.git
* tomcat job- https://github.com/linuxacademy/content-jenkinscert.git

**Objectives**
* Create webdev/index and archive index.jsp:
  * Configure Maven M3.
  * Create webdev folder.
  * Configure the job to take parameters, name=steve.
  * Pull from git using url that is in the instructions.
  * Build top level maven 'clean package'.
  * Shell run bin/makeindex.
  * Archive index.jsp.
* Create backend/tomcat trigger it to build on index complete > succesful:
  * Create backend folder and tomcat subfolder.
  * Create tomcat frestyle project.
  * Configure trigger on index successful.
  * Pull from git Url is in instructions.
  * Build top level maven 'clean package'.
  * Make sure that it runs after index completes.
  * Check index for steve.
