### Exposing Container Ports to the Host

1. Create a container from the 'centos:cetnos6' base image on your system. This container does not need to be name but should be run in daemon mode, interactive and connected to the current terminal. Finally, it should start the bash shell on start up

2. Using the appropriate Docker inspection command, find the IP address and name for the running container. Once you have the IP, ping the IP to be sure it is running. Finally, attach to the running container so you are logged into the shell.

3. From within the container, install the Open-SSH server and make sure the service is running. From another terminal, try to log into the container over SSH by IP and note the result.

4. Exit and stop the container. Remove the container from the list of previously run containers once you obtain the name from the appropriate Docker command.

5. Create another container, name this container 'test_ssh'. When creating the container, it should be run in interactive mode and attached to the current terminal running the bash shell. Finally, expose port 22 on the container to port 8022 on the host system. Once logged in, install the Open-SSH server and make sure the service is running. Find the IP address of the container and note it.

6. Install the 'sudo' utility. Add a user called 'test' and set a password for that user. Add the 'test' user to the 'sudoers' file. From another terminal window, attempt to log into the container via SSH as the 'test' user and confirm access.
