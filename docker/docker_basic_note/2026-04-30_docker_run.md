<h1>Docker Run</h1>
We learned that we can use the Docker run Redis command to run a container running a Redis service.
 ```console
 $ Docker run redis
 Using default tag: latest
 latest: Pulling from library/redis
 f5d23c7fed46: Pull complete
 Status: Downloaded newer image for redis:latest
 
 1:C 31 Jul 2019 09:02:32.624 # oO00oO0OoO0Oo Redis is starting oO00oO0OoO0Oo
 1:C 31 Jul 2019 09:02:32.624 # Redis version=5.0.5, bits=64, commit=00000000, modified=0, pid=1, just started
 1:M 21 Jul 2019 09:02:32:626 $ Server initialized
 ```
 In this case, we know that docker is running the lastest version of Redis version `5.0.5` but what is we want to run another version of Redis that is a older version. 

<h3>Running Image Version in Docker</h3>
To run a specific version on a image, we have to use the `docker run` command with the `image version` and finally the version separated by a colon.
 ```console
 $ docker run regis:4.0
 Unable to find image 'redis:4.0' locally
 4.0: Pulling from library/redis
 e44f086c03a2: Pull complete
 Status: Downloaded newer image for redis:4.0

 1:C 31 Jul 2019 09:02:56.527 # oO00oO0OoO0Oo Redis is starting oO00oO0OoO0Oo                                                                                                                                                                                                    
 1:C 31 Jul 2019 09:02:56.527 # Redis version=4.0.14, bits=64, commit=00000000, modified=0, pid=1, just started                                                                                                                                                                   1:M 21 Jul 2019 09:02:56:530 $ Server initialized         
 ```
 Regis:4.0 is an example of `Tag`. A tag is a market that helps you identify and differentiate between various states or vairent of an image within a repository.
 In our case, Docker has pulled version 4.0 of regis and runs it. If we don't specify any tag when running the image, Docker will run the latest image.

<h3>How to find supported tags for a image</h3>
Visit Docker hub, and look up an image and there will be all the supported tags in it description. Each version of the software can have multiple short and long tags associated with it. 
 ```console
 $# example of short and long tags

 5.0.5, 5.0, 5-buster, buster 
 5.0.5-32bit, 5.0-32bit, 5-32bit-buster, 32bit-buster 
 5.0.5-alpine, 5.0-alpine, 5-alpine. alpine
 4.0.14, 4.0, 4, 4.0-buster, 4-buster
 ```
<h3>Input</h3>
A simple prompt application when run it ask for your name and after entering your name. It will print a welcome message.
 ```console
 $ ~/prompt-application$ ./app.sh
 Welcome! Please enter your name: Prosper
 
 Hello and Welcome Prosper!
 ```
However, when we put this application in Docker and run it as a Docker container, it wouldn't wait for the prompt. It just prints whatever the application is supposed to print on standard out.
```console
 $ docker run kodekloud/simple-prompt-docker

 Hello and Welcome !
 ```
By default, the Docker container does not listen to standard input. Even though you're attached to its console, it is not able to read any input from you. It doesn't have a terminal to read inputs from; it runs in a non-interactice mode.
If you want to provide your input, you must map the standard input of your host to the Docker containers using the `-i` parameter. 
 ```console
 $ docker run -i kodekloud/simple-prompt-docker
 Prosper

 Hello and Welcome Prosper!
 ```
`-i` parameter is for interactive mode. And when you input name, it prints the expected output. However, there is something that is missing. Which is the prompt: "Welcome! Please enter your name:"
That is because the application prompt is not on the terminal, and we have to attached it to the container's terminal. For this, we use the `-t` parameter.
 ```console
 $ docker run -it kodekloud/simple-prompt-docker
 Welcome! Please enter your name: Prosper

 Hello and Welcome Prosper!
 ```
`-t` stands for a pseudo terminal. With the combination of `-i` and `-t`, we're now attachec to the terminal, as well as in an interactive mode on the container. 
