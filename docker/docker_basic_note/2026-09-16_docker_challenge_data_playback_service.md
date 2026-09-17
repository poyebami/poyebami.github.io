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

<h3>WORKDIR</h3>
This set the working directory inside the `container`. All subsequent COPY/RUN commands operate relative to this, and it's where the container starts when its runs. Docker creates the folder if it doesn't exist. 
 ```console
 WORKDIR /home/propser/devops-challenge
 ```

<h3>COPY</h3>
This copies requirements.txt from my host project folder into the container's working directory.

It is a command used to inject application source code, configuration files, and dependencies into an image.
 ```console
 COPY requirements.txt .
 ```
<h3>RUN</h3>
This pretty much says to install all dependencies that are listed in `requirements.txt` but to also remove download caches.
 ```console
 RUN pip install --no-cache-dir -r requirements.txt
 ```
<h3>COPY</h3>
Copies the package folder. Both __init__.py and __main__.py into the container. 

__init__.py file is used to mark a directory as a regular Python package and to execute initialization code when that package is imported. 

In our case __init__.py marks data_playback as a Python package, which is what lets you run it as python -m data_playback. Copying the files loose would break it.
 ```console
 COPY data_playback/ ./data_playback/
 ```
<h3>RUN</h3>
 This creates a non-root user named appuser inside the container. -m also creates a home directory for them at /home/appuser.

 The reason is becuase by default containers run as root, which is a security concern. If something compromises your app, it's running with full privileges inside the container.
 ```console
 RUN useradd -m appuser
 ```
<h3>User</h3>
This switches to appuiser for everything after this line, including whatever the container runs as startup.

WORKDIR and copied files were created while running as root, so appuser doesn't own them. If your script ever need to write into the directory, you'll get "permission denied".
 ```console
 $ # permission denied
RUN useradd -m appuser && chown -R appuser:appuser /home/propser/devops-challenge
USER appuser
 ```
<h3>ENTRYPOINT</h3>
ENTRYPOINT : sets the command that always runs when a containers starts from this image. 
 ```console
 ENTRYPOINT ["python", "-m", "data_playback"]
 ```
 Python - the program being run ( the python interpreter)
 -m - a play telling Python "run a module/package by name, not a file path." This is what lets you invoke the whole packge (folder with __init__.py) rather than pointing at one specific .py file. 
 data_playback - the name of the package to run. Python looks for a folder named data_playback (found via WORKDIR), since that's where it was copied to) containing an __init__.py (marks its as package) and specifically looks for __main__.py inside it as the entry point to execute. 

 Pretty much says : "find the data_playback package, and run its __main__.py"
