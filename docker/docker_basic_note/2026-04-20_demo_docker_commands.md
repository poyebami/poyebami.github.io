<h1>Demo Docker Commands</h1>

<h3>Running images</h3>
When running official images, you just need to write the name of the images.
 ```console
 $ docker run ubuntu
 ```
When running your own images, you need to running it using the user id and then followed by the forward slash and the name of the repository.
 ```console
 $ docker run prosper/test-repos
 ```
<h3>How to know you are inside a container</h3>
You will see a prompt that says the root @ with a unique id.
 ```console
 $ docker run -it ubuntu bash
 [root@e0ae1ec7e1d3 /] #
 ```
<h3>Exit from a container</h3>
Use the exit command
 ```console
 [root@e0ae1ec7e1d3 /] # exit
 ```
<h3>Docker ps command</h3>
List all the running containers
 ```console
 $ docker ps 
 ```
To see all the containers you ran in the past and all the exited containers, use the `ps command with -a`
 ```console
 $ docker ps -a 
 ```
<h3>Stop a container</h3>
Running docker stop command with the name or id of the container
 ```console
 $ docker stop serene_pasteur

 $ docker stop 132n129a1qd
 ```
You can also see the exit code after a container has exited using the `ps -a command`. Since we stopped the recent container with a stop command, the exit code is `137`. The exit code for the other containers are `0` because they exited
under normal conditions. 

<h3>Removing containers </h3>
There are lots of containers we see when we running `docker ps -a` and we want to remove them. Use `docker rm command` with the unqiue id or name of the container.
 ```console
 $ docker rm 181329fd841
 181329fd41

 $ docker rm silly_goose
 ```
To remove muitiple containers, just add the container ids to the `rm command`
 ```console
 $ docker rm 181 3o1 592
 181
 3o1
 592
 ```
<h3>Show all images installed</h3>
To see the images that you currently have, use the `docker images` command.
 ```console
 $ docker images
 REPOSITORY             TAG         IMAGE ID            CREATED         SIZE
 ubuntu                 latest      ccc7a11d65b1        9 days ago      120MB
 hello-world            latest      1815c82652c0        2 months ago    1.84kB
 ```
<h3>Removing images</h3>
To remove docker images use the `docker rmi` command with the name of the image
 ```console
 $ docker rmi hello-world
 ```
 `rm` is for removing containers while `rmi` is for removing images

 If you try to delete a docker image that is being used by a container, the `rmi command` will `fail`. You will need to remove all the containers first before removing the image. 

<h3>Difference between Run and Pull commands</h3>
When we ran the docker run command with Ubuntu, it first looks for an image locally. If the image is not locally, its going to pull the image and immediately run a container with that image. 
If we don't want docker to run immediately and just pull the image, use the `docker pull` command. 

<h3>Running a command in a container</h3>
To run a command in a container use the `docker exec` command with the id of the container followed by the `command you want to run`.
 ```console
 $ docker exec c1a19de cat /etc/*release*
 ```
 Exec means execute
