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

