### Security in Jenkins

The company has failed a security audit and it has been determined that stricter security needs to be implemented on all servers and services, this includes the Jenkins server. To this end you will need to create folders for the jobs that are on the jenkins server. There are 3 users that need to be on the server:
* James is the web developer and his projects need to be in the webdev folder so that only James can access them. 
* Diane is the manager of backend development and needs access to the backend folder and all jobs in that folder and all children of that folder. 
* Laura is a new developer on the backend team and has been hired to get the tomcat project back on track. She will require access to the backend/tomcat folder and all jobs in that folder. 

You will need to create these folders and some dummy jobs to ensure that the permissions are correct and that only the required access is given.

**Objectives**
* Enable Project based matrix security:
  * go to manage jenkins > global security and enable project based matrix seecurity. Ensure that authenticated users have global read access at this level.
* Create users, James, Diane and Laura:
  * Go to manage jenkins > manage users and create accounts for James, Diane and Laura.
  * Remember the passwords so that you can Audit secrity as you set it.
* Create webdev folder and give James access:
  * Create a top level folder named webdev.
  * Enable project security and disallow inheritance.
  * Add james and give him full access.
* Make a freestyle project named test, and set it to inherit from parent:
  * Create backend folder and give Diane full access.
  * Create a top level folder named backend, in the folder config enable project based security.
  * Disable inheritance and add Diane and grant full access
* Create tomcat folder inside the backend folder and give Laura access to this folder:
  * Go into the backend folde, create a new item, create a folder named tomcat.
  * On this folder configure project based security and add laura with full access and alllow inheritance from parent.
  * Make sure that on the backend folder Laura has permissons to view job so that she can see the tomcat folder.
  * Inside tomcat make a test freestyle project.
* Verify that James is not able to access the backend folder, Diane cannot see the webdev folder but can see tomcat, Laura can only access tomcat.
  * Login as each user and attempt to access the folders that they should not be allowed access to.
