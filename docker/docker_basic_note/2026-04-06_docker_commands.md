<h1>Docker Commands</h1>

<h3>Basic Docker Commands</h3>
Docker run command is used to run a container from an image.
 ```console
 $ # run an instance of the Nginx application on the docker host
 $ docker run nginx
 ```
If the image is not present on the host, it will go out to Docker Hub and pull the image down. 

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
 cff8ac918a2f       redis       "docker-entrypoint.s.."     6 seconds ago       Exited (0) 3 seconds ago 
 ```


