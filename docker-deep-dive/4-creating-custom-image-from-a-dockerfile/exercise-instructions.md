### Creating Custom Image from a Dockerfile

1. Create a directory called 'custom' and change to it. In this directory, create an empty file called "Dockerfile". 
2. Edit the "Dockerfile" created in Step #1 above. This configuration file should be written to perform the following actions:
* Use the base Centos 6 Latest version image from the public repository
* Identify you and your email address as the author and maintainer of this image
* Update the base OS after initial import of the image
* Install the Open-SSH Server
* Install Apache Web Server
* Expose ports 22 and 80 to support the services installed
3. Build the custom image from the 'Dockerfile' as created above. Name/tag this new image as "mycustomimg/withservices:v1". Once the image is built, verify the image appears in your list.
