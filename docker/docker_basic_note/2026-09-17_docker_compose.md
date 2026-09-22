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
`Depends_on` : tell compose "this service relies on another service. In our case, `data_redactor` relies on `data_playback.` 
You can also list multiply services. 
 ```console
 depends_on:
    - data_playback
    - some_other_service
 ```
 
`Volume`: is used to share/link a folder (or file) between your hosr machine and the container's filesystem.

This is needed because the containers are isolated.  With -v or volume, the python scripts tries to read /data/output.mp4 but the path wouldn't exist inside the container and will fail because __output.mp4__ has failed. The volume mount makes your host's data/ folder appears inside the container at the path you specify, so the scripts can find and read the file. 
In our case, -v/ volume will let data_playback (running inside its isloated container) actually access the output.mp4 file. 
<h3>Build</h3>
Build the image from the Dockerfile in the current directory.

It is equivalent to docker build -t ....

<h3>Ports</h3>
The same as -p in docker run.

<h3>Volume</h3>
The same as -v in docker run.

<h3>Environment</h3>
The same as -e in docker run. 
