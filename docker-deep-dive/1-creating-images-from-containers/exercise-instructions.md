### Installation and Image Setup

1. Update your system as appropriate for the distribution you are using. Use the instructions in the videos OR on the Docker site to add the DOCKER repository for installing the latest copy of Docker for your distribution and version.
2. Using the appropriate package management commands, install the 'docker' package. Once installed, enable the service so that it starts upon reboot. Additionally, start the 'docker' service and verify it is running.
3. Enable the non-root users to run 'docker' commands on the system. Create the appropriate group, add the users you want to have access to 'docker' commands, restart the 'docker' service and verify that non-root users can run basic 'docker' commands.
4. Once 'docker' is installed and non-root users can run commands, use the appropriate 'docker' commands and options to download the latest available image in the public repository for Ubuntu. Once downloaded and installed, verify the image appears in the local base image list.
5. Start a container based upon the Ubuntu base image downloaded in Step #4. When you start the container, start it connected to the current terminal, in interactive mode, starting the bash shell for you to connect to. You may exit the container at that time.
