<h1>Creating a Dockerfile</h1>
To create a Dockerfile, you need to create a plain text file named DockerFile (with no file extension and a capital D)
 ```console
 touch Dockerfile
 ```
<h2>Instruction after creating a Dockerfile</h2>

<h3>FROM</h3>
The first line of a Dockerfile is going to be `FROM`. `FROM` specifices what base image, we'll be using to build our own image.
 ```console
 FROM <image>:<tag>
 FROM node:20-alpine

 FROM ubuntu:24.04
 FROM ubuntu:jammy
 FROM nginx:latest
 FROM nginx:1.31.4-alpine
 ```
Note: I used hub.docker.com to find Docker images and also their tags. `Alpine` is a lightweight linux operating system that is used because it is small (5MB) and boots fast. 

<h3>ENV</h3>
`ENV` is instruction sets environment variables that presist both during the image build process and when the container is running.
 ```console
 ENV key=value
 ```
<h3>COPY</h3>
`COPY` instruction in a Dockerfile copies files and directories from your host machine into the filesystem of the Docker image during the build process.
 ```console
COPY <source> <desination>

$ # copying a single file
COPY requirement.txt /app/requirement.txt
$ # copying multiple files
COPY *.json /app/
$ # copying an entire directory
COPY src/ /app/src/
 ```
