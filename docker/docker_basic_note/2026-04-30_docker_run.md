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

<h3>Run - PORT mapping </h3>
Running a web application in a Docker container on Docker Host
 ```console
 $ docker run kodekloud/webapp
  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
 ```
The underlying host where Docker is installed is called Docker host or Docker Engine. When we run a containerized web application, it runs and we are able to see that the server is running.
However does a user access the application. The appliction is listening on port `5000`. I can access my application using port `5000`. But what IP do I use to access it from a web brower? 

There are two options available. One is to use the IP of the Docker container. Every container gets a IP assigned by default. In this case, its 172.17.0.2. 

To get the IP address of a Docker container run
 ```console
 $ docker inspect \ -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_nameor_id
 172.17.0.2
 ```
`NOTE:` This is a internal IP and is ONLY accessible within the Docker host. So if you open a browser from within the Docker host, you can go to HTTP://172.17.0.2:5000 to access the IP address. 
However sicne this is a internal IP, users outside of the Docker host cannnot access it using this IP.

For this, we could use the IP of the Docker host. In this case, it is 192.168.1.5. However, for that to work, you must have mapped the port inside the Docker container to a free port on the Docker host. 
If I want a user to access the application through `port 80` on my Docker host, I could map port 80  of localhost to port 5000 on the Docker container using the `-p` parameter in my run command.
 
`-P` stands for `port mapping or port publishing`. It connects a port on your host machine to a port inside the container.
 ```console
 $ docker run -p 80:5000 kodekloud/webapp
 ```
The application inside the container is listening on port 5000. Docker maps it so you can access it through port 50 on your machine. Containers are isolated, so withouht `-p`, you can't access the application from your brower even if its running. 
The user can aceess the application by going to the URL HTTP://192.168.1.5:80. All traffic on `port 80` on my Docker host will get routed to `port 5000` inside the Docker container. 

You can run multiple instances of your application and map them to different ports on the Docker host or run instances of differenet applications on different ports.
 ```console
 $ docker run -p 80:5000 kodekloud/webapp
 $ docker run -p 8000:5000 kodekloud/webapp
 $ docker run -p 8001:5000 kodekloud/webapp
 $ docker run -p 3306:3306 mysq1
 $ docker run -p 8306:2206 mysq1
 ```
You can run as many application like thiat and map them to as many ports as you want. You cannot map to the same port on the Docker host more than once.

<h3>PORT MAPPING EXAMPLE</h3>
Run an instance of kodekloud/simple-webapp:blue and name the container blue-app, mapping port 8080 on the container to port 38282 on the host.
 ```console
 docker run -p 32828:8080 --name blue-app kodekloud/simple-webapp:blue
 ```

<h3>Run - Volume mapping </h3>
Looking into how data is persisted in a Docker container. 
 ```console
 $ docker run mysq1
 ```
We run a mysq1 container. When databases and tables are created, the data files are stored in location `/var/lib/mysq1` inside the Docker container. 
For example: we dump a lot of data into the database and deleted MySQL container and remove it. The container along with all the da ta insdie it is gone. You would like to persist data, you would want to map a directory outside the container on the Docker host to
a directory inside the container. 
 ```console
 $ docker run -v /opt/datadir:/var/lib/mysq1 mysq1
 ```
In this case, we created a directory called /opt/datadir and map that to /var/lib/mysq1 inside the Docker container using the `-v` option and specifying the `directory on the Docker host` followed by a colon and the `directory inside the Docker container.`

<h3>Inspect Coontainer</h3>
Docker ps command is good enough to get basic details and containers like their names and IDs. But if you want to get additioanl details about a specific container, use the Docker inspect command and provide the containers name or ID.
 ```console
 $ docker inspect <containerName_ID>
 $ docker inspect blissful_hopper
 [
    {
        "Id": "35505f7810d17291261a43391d4b6c084..."
        "Name": "/blissful_hooper",
        "Path": "python",
        "Args": [
            "app.py"
        ],
        "State": {
            "Status": "running",
            "Running": true,
        },

        "Mounts": [],
        "Config": {
            "Entrypoint": [
                "python",
                "app.py"
            ],
        },
        "NetworkSetting": {..}
    }
 ]
 ```
It returns all the details of a container in a JSON format, such as the state, mounts, configuration data, network settings. It is important to use it when you're required to find details on a container. 

JSON FORMAT: a lightweight, text-based, language-independent data-interchange format, commonly used for transmitting data between servers, and web applications.

<h3>Container Logs</h3>
For example, you run a simple web application using `-d` parameter and it ran the container in detached mode. How do you view the logs which happens to be the contents written to the standard out of that container? 
Use the docker logs command and specify the container ID or name
 ```console
 $ docker logs blissful_hopper
 This is a sample web application that displays a colored background.
 A color can be specified in two ways.

 1. As a command line argment with --color as the argument. Aceepts one of red, green, blue, blue2, pink, darkblue
 2. As an Environment variable APP_COLOR. Accepts one of the red, gree, blue, blue2, pink, darkblue
 3. If none of the above then a random color is picked for the above list.
 Note: Command line argument precedes over environment variable.
 
 ...
 ``` 
 Docker logs command is used to retrieve and view logs from a specific Docker container. It captures any data the application writes to the standard output (STDOUT) and standard error (STDERR) streams. 
