### Adding External Content to Containers

1. Create a directory in your 'user' home directory called 'docker'. Within that directory, create another directory called 'mydata'. Within that directory, create a file called 'mydata.txt' containing any text message you want.

2. Create a docker container name 'local_vol' from the 'centos:centos6' image. The container should be created in interactive mode, attached to the current terminal and running the bash shell. Finally create the container with a volume (or directory) called 'containerdata' so that the system will automatically create the directory/mount when the container starts.

3. List the filesystems within the container, specifically looking for the volume/directory that was added to the container during creation.

4. Exit the container. This time, create another container called 'remote_vol' with the same container configuration except when creating the volume in the container, link the volume name 'mydata' to the underlying host directory structure created in Step #1.

5. Once the container is started, list the disk mounts and verify the remote (host) volume is mounted. Change to that directory and verify that the text file created in Step #1 appears with the content created.
