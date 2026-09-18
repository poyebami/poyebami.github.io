<h1>Docker Compose</h1>
Docker Compose is a tool for defining and running multiple containers together as one coordinated setup, using a single YAML config file instead of typing out long `docker run` commands by hand each time. 

Create a docker-compose.yml file in your project root (same folder as Dockerfile).
 ```console
 version: "3.9"

services:
  data_playback:
    build: .
    ports:
      - "5555:5555"
    volumes:
      - ./data:/home/prosper/devops-challenge/data
    environment:
      - DATA_FILE=/home/prosper/devops-challenge/data/output.mp4
 ```
<h3>Version</h3>
Version - is the compse file format version. (tell Docker how to interpret the syntax below)
```console
 $ version: "3.9"
```
<h3>Service</h3>
Service - lists each container you want to run; you can have one or many. 
Below, we have two example of containers. __data_playback__ and __frame_consumer__ are both the names of the containers.
```console
 version: "3.9"

services:
  data_playback:
    build: .
    ports:
      - "5555:5555"
    volumes:
      - ./data:/home/prosper/devops-challenge/data
    environment:
      - DATA_FILE=/home/prosper/devops-challenge/data/output.mp4

  frame_consumer:
    build: ./consumer
    depends_on:
      - data_playback
    environment:
      - PLAYBACK_HOST=data_playback
      - PLAYBACK_PORT=5555
```
<h3>Build</h3>
Build the image from the Dockerfile in the current directory.

It is equivalent to docker build -t ....

<h3>Ports</h3>
The same as -p in docker run.

<h3>Volume</h3>
The same as -v in docker run.

<h3>Environment</h3>
The same as -e in docker run. 
