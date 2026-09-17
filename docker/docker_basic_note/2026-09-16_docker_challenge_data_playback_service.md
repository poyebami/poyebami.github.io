<h1>Docker Challenge: Data Playback Service</h1>
The point of this container is to take a video from the internet and split each frame into images, and then publishes that image dataset with some packed metadata (width and height). The publisher is using ZeroMQ.

I started with creating a Dockerfile.
 ```console
 FROM python:3.12-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    libgl1 \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /home/propser/devops-challenge

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY data_playback/ ./data_playback/

RUN useradd -m appuser
User appuser

ENTRYPOINT ["python", "-m", "data_playback"]
 ```

<h3>FROM</h3>
```console
FROM python:3.12-slim
```
In data_playback, there is a two files called __main__.py and __init__.py files. This is the reason why I picked python image because my code is using python. 

The reason I picked version and tag python:3.12-slim is because I'm using a version that because my code will run on the exact same back environment every time it is build or deployed. If I were to use a latest version, it will frequently updates and could break the container. 

I used silm becuase it is a trimmed down Debian variant. It removes the extra tools, docs, compilers, and etc I don't need.

<h3>RUN</h3>
 ```console
 RUN apt-get update && apt-get install -y --no-install-recommends libgl1 libglib2.0-0 && rm -rf /var/lib/apt/lists/*
 ```
1. I used apt-get update to refreshes the package index so apt knows what's available. 
 ```console
 apt-get update
 ```
2. -y is used to auto-confirm the install prompt. Without it, when docker build will not work.

3. I used this to skip optional "suggested" packages, keeping the image smaller. 
 ```console
 --no-install-recommands
 ```
4. libgl1 and libglib2.0-0 is because without them import cv2 in __main__.py will fail. 
 ```console
 ImportError: libGL.so.1: cannot open shared object file
 ```
 You get this error becuase the code is missing the core OpenGL library, which Python pakcages like OpenCV(cv2) need to render graphics. 

5. rm -rf /var/lib/apt/lists/* This is used to delete the downloaded packages index afterwards so its doesn't bloat the final image (Debian's equivalent of Alpine's --no-cache)
 -r : "recursive" needed to delete a directory and everything inside it. Just rm will only delete individual files, not folders.
 -f : "force" is used to suppresses confirmation prompts and doesn't error out if a file doesn't exist.
 
 It pretty much means "delete this, and everything inside it, without asking me to confirm, and don't complain if something's already missing". 

 ```console
 $ # this is every apt-get update stores packages index files downloaded from remote repositories.
 /var/lib/apt/lists/*
 ```
 "*" at the end means "everything inside this folder" not the folder itself. 
 In this case, delete everything inside this folder but not the folder itself. 
 
