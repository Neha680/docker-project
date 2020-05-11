# docker-project
infrastructure project based on docker

Pre-requisites:
1. OS: Redhat Enterprise Linix 8 or Centos8
2. Docker Engine
3. Docker-compose

![1](https://user-images.githubusercontent.com/64469502/81547094-fac8d800-9398-11ea-81af-b0dfa8028943.jpg)


Implementation Steps

Follow the below steps to successfuly configure the automation of Project:

	1. Clone master branch of the repository

	2.Copy the files inside source_code directory in NFS mounted directory.

There are two ways to mount the code inside both the application_servers:

	*Make a seperate directory named NFS i.e

		mkdir /nfs
	In the docker-compose.yml file, replace nfs_storage variable wth /nfs in volumes option in nfs_server.

	volumes:
  		- /nfs:/nfsshare
	Deploy the code inside /nfs/apps directory.

	*Find out the mount-point of the nfs_storage volume using docker volume management command

 		docker volume inspect $(docker volume ls | grep nfs_storage | awk '{print $2}')   
	
	Copy the code inside the mount point to share the application code among application_containers.

Note:

The application server containers won't boot up until the code deployment is successful

	3. Execute the docker-compose command
		docker-compose up -d
	-d parameter to run the containers in the background.

	4. Services should be up now.



Source: LinuxWorld Informatics Pvt Ltd. Jaipur

Under the Guidance of : Vimal Daga

Initiative: IIEC-RISE
