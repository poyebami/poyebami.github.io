<h1>Containers</h1>
Docker containers are isolated environments. They can have their own processes, network, and mounts, just like virtual machines. They all share the same operating system kernel. A container is lightweight and executable packages of software that includes everything needed to run an application - code, runtime, system tools, system libraries, and settings. It allows developers to bundle an application with its entire ecosystem so it run identifcally on any machine.

<h3>Port Mapping</h3>
Port mapping allows external traffic from your host machine or the internet to reach applications running inside an isolated Docker container. By default, containers ports are completely blocked from external access. 
 ```console
 $docker run -p <HOST_PORT>:<CONTAINER_PORT><IMAGE_NAME>
 ```
 HOST_PORT: The port you can open on your local computer/server to access the app
 CONTAINER_PORT: The internal port that applications is listening on inside the container. 

 ```console
 $ # maps traffic from your host's port 8080 to the container's standard web port 80.
 $ docker run -d -p 8080:80 nginx
 ```
<h3>Docker Volume</h3>
Docker volume maps files system on a host machine to file system on a Docker container. 

<h4>Docker Create Volume</h4>
 ```console
 $ # create a docker volume
 $ docker volume create <VOLUME_NAME>
 $ # let docker create a anonymous docker volume 
 $ docker volume create
 ```
<h4>List all docker volume</h4> 
 ```console
 $ # list all docker volume
 $ docker volume list
 ```
<h4>Remove Docker volume</h4>
 ```console
 $ # removing docker volume
 $ docker volume rm <VOLUME_NAME>
 
 $ # remove all local volume not used by at least one container
 $ docker volume prune
 ```



