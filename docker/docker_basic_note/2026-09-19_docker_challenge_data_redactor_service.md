<h1>Docker Challenge: Data Redactor Service </h1>
The point of this container is to redacts the outer frame of image from data playback. Then it publishes that data on  a new ZeroMQ socket.

I stared with creating a Dockerfile.
 ```console
FROM python:3.12-slim

WORKDIR /home/prosper/devops-challenge

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY data_redactor/ ./data_redactor

RUN useradd -m appuser && chown -R appuser:appuser /home/prosper/devops-challenge

ENTRYPOINT ["python", "-m", "data_redactor"]
 ```
I picked python:3.12-slim because my code is using python.

My working directory inside the contaienr is /home/prosper/devops-challenge.

It copies requirements.txt to the current directory from my host project into the container's directory.

RUN pip installs all my dependencies that are listed in requirements.txt. `-r` means to read.

Copies data_redactor package folder into the container.

RUN useradd creates a user called appuser and gives permission /home/prosper/devops-challenge

ENTRYPOINT ["python", "-m" "data_redactor"]

<h1>Building the image</h1>
 ```console
 docker build -t data_redactor . 
 docker build -f data_playback/Dockerfile -t data_playback . 
 ```
