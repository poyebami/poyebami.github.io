<h1>Docker Commands - Part 1</h1>

<h3>Docker run command</h3>
When running on docker run <image>, if you don't have the image locally, it will automatically download(pulls) the images from a remote container registry.

<h3>Running a docker image in the background</h3>
To run a docker image in the background use `-d`
 ```console
 $ # run the image in background (detached mode)
 $ docker run -d nginx
 $ # output: prints the container ID
 ```
When in detached mode, Docker will starts in the background and immediately give you back your terminal prompt, instead of attaching your terminal to the container's output.
Without `-d`, the terminal would attach to the container, and you'd see nginx's log output live - but the terminal would be "stuck" running the container in the foreground until you stop it . `ctrl+C`

<h3>List all running container</h3>
  ```console
  $ # list all `running` containers
  $ docker ps
  ```
It see all containers that are running , stopped, and exited, use the docker `ps` command with `-a`
 ```console
 $ # list all running, stopped, and exited containers
 $ docker ps -a
 ```
<h3>Stop a container</h3>
To stop a running container, use the docker `stop` command with the container ID or the Name
 ```console
 $ # stop running containters using the ID
 $ docker stop ecce
 $ # output: prints out the container ID

 $ # stop running container using Name
 $ docker stop beatiful_boyd
 $ # output: prints out the container Name
 ```
 <h3>Delete and remove container</h3>
 To remove containers, use the docker rm <image> (container ID or Name)
  ```console
  $ # remove one container
  $ docker rm amazing_moore
  $ # output: amazing_moore

  $ # remove muitiple containers
  $ docker rm af11 8dd1 sdf1
  $ # output: af11
  $ # output: 8dd1
  $ # output: sdf1
  ```
