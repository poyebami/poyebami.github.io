<h1> Creating your own Docker Image </h1>
To start your first docker image, you need to create a `DockerFile`. 

<h3>FROM</h3>
After creating your DockerFile, the first thing you must do is type `FROM` on the file. The `FROM` instuction in a DockerFile is the foundation of an image, used to define the Base Image upon which all subsequent instructions are built. 

Think of it like choosing a starting point. Instead of building an OS and runtime from scratch, you start with an existing image and add your stuff on top. When picking a base image, you can pick whatever version you want using tags and getting the base image name from Docker Hub.
 ```console
 FROM <image>:<tag>
 $ # examples 
 FROM ubuntu
 FROM ubuntu:22.04
 FROM ubuntu:rolling
 FROM ubuntu:questing-20251217
 FROM nginx
 ```
When picking a docker image for a project, make sure the image best fits what you are doing. For example, some images are too big and run slow. Some that are small and run fast however it may not have what you need to execute your project and you have to install extra things instead of it. 

Another thing when using a docker iamge with latest tag is that it is a "moving" target. Latest is always changing. For example, months after using a latest tag, it maybe a different from version that you test months ago. In between those months something may have change that breaks your project. It very hard to debug later, since you don't know which version was used. 
 ```console
 it best to use a image with a version tag. For example
 FROM alpine:3.20
 when using a version tag, anyone build the dockerfile months, years, from now will get the same results.
 ```
<h3>RUN</h3>
The `RUN` instruction execute commands during the image build phase to set up the container's environment. It is mainly used to install software packages. download dependencies, create direcotires and configure system. 

RUN has two distinct formats. 
1. Shell Form: executes the command inside a shell environment. This form supports shell features like environment variables, piping, and command chaining (&&).
 ```console
 RUN apt-get update && apt-get install -y curl
 $ # this command just checkes the local list for updates packages and install curl. -y auto confirms "Do you want to continue?[Y/n]" prompt. 
 ```
2. Exec Form: parses the instruction as a JSON array and executes the binary directly without invoking a shell. Use this if you need to run commands using a specific shell or avoid shell string processing. 
 ```console
RUN ["apt-get","update"]
$ # " get and update"
 ```
APT is the package manager for ubuntu. There use YUM, APK, etc. A package manager is a tool that automates installing, upgrading, configuring, and removing software on your computer or in a project.

<h3>WORKDIR</h3>
WORKDIR instruction in a Dockerfile sets the working directory for any subsequent RUN, CMD, ENTRYPOINT, COPY, and ADD instructions. It functions exactly like a `cd` command inside the container filesystem, ensuring that all following operations take place in that specified folder.
 ```console
# $ WORKDIR sets the active working directory inside the container to a folder named /download
WORKDIR /download
 ```
Think of it as the command line equivalent of running cd /download.
<h3>ENTRYPOINT</h3>
Entrypoint is a dockerfile instruction that sets the fixed command that always runs when a container starts from that image. Whenever arguments you pass to `docker run`  get appended to it, rather than replacing it. 
 ```console
 ENTRYPOINT ["curl", "-L"]
 $ Every time you run a container from this image. Docker execute curl -L first, then appends whatever arguments you pass at the end of your docker run command.
 ```
<h3>Conclusion</h3>
Once you are finished with create your DockerFile, use the command `docker build` to turn it into a usable image.
 ```console
 $ # turns dockerfile into a image
 $ docker build

 $ # -t is a flag "tag" that give the resulting image a name

 $ docker build -t curl-mp4 . 
 $ # use docker images command to see the image you created
 $ # build a image called curl-mp4 in current directory
 ```
