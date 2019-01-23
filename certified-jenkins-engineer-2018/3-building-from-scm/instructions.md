### Building from SCM

Your company is ready to start utilizing the jenkins server that you installed. The first project that they would like to convert to run on jenkins is a maven project from your companies M3 maven server. This is to replace that server, but projects built there have the instance name hardcoded. You are to create a project named 'mavenproject'. This should pull the code from the git repo and build the project. This should include the call to binary that creates the index.jsp file. bin/makeindex The index.jsp file needs to be tracked for version control purposes.

1. The URI of the git repository for this lesson: https://github.com/linuxacademy/content-cje-prebuild.git
2. The shell command required to produce the index.jsp:
```bash
filebin/makeindex
```

**Objectives**
* Configure Maven Installer.
* Configure the build to use Maven and produce the index.jsp file.
