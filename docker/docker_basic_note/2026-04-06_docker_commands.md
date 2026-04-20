<h1>BasicDocker Commands</h1>

<h3>Docker run command</h3>
Docker run command is used to run a container from an image.
 ```console
 $ # run an instance of the Nginx application on the docker host
 $ docker run nginx
 ```
If the image is not present on the host, it will go out to Docker Hub and pull the image down. 

<h3>Docker list command</h3>
Docker ps command lists all running containers and some basic information, such as the container ID, the name of the iamge we use to run the containers, the current status and the name of the container.
Each containers automatically gets a random ID and name created for it by  Docker, which in this case is Silly Summit.
 ```console
 $ docker ps
 
 CONTAINER ID       IMAGE       COMMAND                     CREATED             STATUS          PORTS       NAMES
 796856ac413d       nginx       "nginx -g 'damon of..."     7 seconds ago       Up 6 second     80/tcp      silly_sammet
 ```
To see all containers running or not use the -a option and outputs all running as well as previosuly stopped or exited containers.
 ```console
 $ docker ps -a 
 CONTAINER ID       IMAGE       COMMAND                     CREATED             STATUS                      NAMES
 796856ac413d       nginx       "nginx -g 'damon of..."     7 seconds ago       Up 6 second                 silly_sammet
 cff8ac918a2f       redis       "docker-entrypoint.s.."     6 seconds ago       Exited (0) 3 seconds ago    relaxed_aryabhata
 ```
<h3>Docker stop command</h3>
To stop a running container use the Docker stop command, but must use either the container ID or the container name in the stop command.
 ```console
 $ docker stop silly_sammet
 silly_sammet
 ```
To check if the running container has stopped, use the command docker ps -a
 ```console
  $ docker ps -a 
  CONTAINER ID       IMAGE       COMMAND                     CREATED             STATUS                       NAMES
  796856ac413d       nginx       "nginx -g 'damon of..."     7 seconds ago       Exited (0) 3 seconds ago     silly_sammet
  cff8ac918a2f       redis       "docker-entrypoint.s.."     6 seconds ago       Exited (0) 3 seconds ago     relaxed_aryabhata
 ```
<h3>Docker remove command</h3>
To remove a stopped or exited container permanently to the docker rm command with the container ID or the container name. It is prints the name back, it worked.
 ```console
  $ docker rm silly_sammet
  silly_sammet
 ```
To check if the container has been removed use the docker ps -a to confirm. 

<h3>Docker list command</h3>
To see the list of available images and their size. Run the docker image command
 ```console
  $ docker images
  REPOSITORY        TAG         IMAGE ID            CREATED         SIZE
  nginx             latest      f68de55e065         4 days ago      109MG
  redis             latest      4760dc956b2d        15 months ago   107MG
  ubuntu            latest      f975c5035748        16 months ago   112MB
  alpine            latest      3fd9065eaf02        18 months ago   4.14MB
 ```
<h3>Docker remove image command</h3>
To remove an image that you no longer plan to use, run the docer rmi command
 ```console
 $ docker rmi nginx
 ```
Make sure that no containers are running off of that image before removing the image; you must stop and delete all dependent containers to be able to delete an image.

<h3>Docker pull command</h3>
While `docker pull` will automatically pull an image if its missing from your local cache, `docker pull` is use to pre-download images without actually starting a container.
Docker pull command downloads container images or repositories from a registry.
 ```console
 $ docker pull nginx
 Using default tag: latest
 latest: Pulling from library/nginx
 fc7181108d40: Pull complete
 d2e987ca2267: Pull complete
 0b760b431b11: Pull complete
 Digest: 
 sha256: 96fb26166270b900ea5a2c17a26abbbfabe98806e73c3a3c65869a6db83223a
 Status: Download newer image from nginx:latest
 ```
Unlike virtual machines, containers are not meant to host an operating system, containers are meant to run a specific task or process such as to host an instance of a web server or application server, or a database, or simply to carry some kind of computation or analysis task. Once the task is complete, the container exits. A container only lives as long as the process inside it is alive. If the web service inside the container is stopped or crashed, then the container exits. This is why  when you run a container from an Ubuntun image, it stops immediately. Because Ubuntu is just an image of an operating system that is used as the base image for other applications. There is no process or application running in it by default. You could instruct Docker to run a process with the Docer run command...

<h3>Docker sleep command</h3>
It runs the sleep command with the duration of five seconds. When the container starts, it runs the sleep command and goes into sleep for five seconds, post which the sleep command exits and the container stops. 
 ```console
 $ docker run ubuntu sleep 5
 ```
This is executing a command when we run the container. 

<h3>Exec- execute a command</h3>
The Docker exec command to used to execute a command on the docker container. 
 ```console
 $ docker exec distracted_mcclintock cat /etc/hosts
 127.0.0.1      localhost
 ::1        localhost ip6-localhost ip6-loopback
 fe00::0 ip6-localnet
 ff00::0 ip6-mcastprefix
 ff02::1 ip6-allnodes
 ff02::2 ip6-allrouters
 172.18.0.2     538d037f94a7
 ```
 <h3>Run -attach and detach</h3>
When you run a Docker run command like this, it runs in the foreground or in an 'attached mode', meaning you will be attached to the console or the standard out of the Docker container. And you will see the output of the web service on the screen.  You won't be able to do anything else on this console other than view the output until the Docker container stops. It won't respond to your input. 
  ```console
  $ docker run kodekloud/simple-webapp
  This is a sample web application that displays a colored background.
  * Serving Flask app "app" (lazy loading)
  * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
  ```
Press CTRL+C combination to stop the container and the application hosted on the container exits and you get back to your prompt. 

Another option is to run the Docker in the detached mode by providing the -d option. This will run the Docker container in the background mode and you will be back to your prompt immediately. The container will continue to run in the backend. 
  ```console
  $ docker run -d kodekloud/simple-webapp
  a043d40f85fe414...
  ```
Run the Docker ps command to view the running container. 

To attach back to the running container later, run the Docker attach command and specify the name or ID of the Docker container. Remember, if you're specifiying the ID of a container in any Docker command, you can simply provide the first few characters alone,
just so it is different from the other container IDs on the host. In this case, I specify a 043d.
  ```console
  $ docker attach a043d
  ```

