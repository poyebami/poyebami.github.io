<h1>Docker Images</h1>
You can create your own docker images. The reason why you would need to create a image is because you cannot find a component or a service that you want to use as part of your application on Docker Hub. 
Another reason is that the application will be containerized for ease of shipping and deployment. 

<h3>How to create my own image?</h3>
In our case, we are creating an image for a simple web application. 
 ```console
  1. Operating System - Ubuntu
  2. Update the source repositories using the apt command
  3. Install dependencies using the apt command
  4. Install python dependencies using pip command
  5. Copy source code of the application to a location like /opt
  6. Run the web server using "flask" command
 ```
1. We need to create a DockerFile named Dockerfile and write down the instructions for setting up your application in it.
 ```console
   FROM Ubuntu

   RUN apt-get update
   RUN apt-get install python

   RUN pip install flask
   RUN pip install flask-mysql

   COPY . /opt/source-code

   ENTRYPOIINT FLASK_APP=/opt/source-code/app.py flask run
 ```
2. We need to build the image using the Docker build command and specify the Dockerfile as input as well as a tag name for the image.
 ```console
 $ docker build Dockerfile -t prosper/my-custom-app
 ``` 
   This will create an image locally on your system. 
3. To make it available on the public Docker Hub registry, run the Docker push command and specify the name of the image you just created.
 ```console
 $ docker push prosper/my-custom-app
 ```
   This name of the image is my account name, followed by the image name. 

<h3>Dockerfile</h3>
Dockerfile is a text file written in a specific format that Docker can understand. It's in a instruction and argument format.  
 ```console                                                                                                                                                                                                                               
   FROM Ubuntu

   RUN apt-get update
   RUN apt-get install python

   RUN pip install flask
   RUN pip install flask-mysql

   COPY . /opt/source-code

   ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
 ```
In this Dockerfile, everything on the `left in caps` is an `instruction`. Each of these instruct Docker to perform a specific action while creating the image. 
 ```console
 FROM 
 RUN
 COPY
 ENTRYPOINT
 ```
Everything on the right is an argument to those instructions. 

<h3>Dockerfile Step-by-Step</h3>
Every Docker image must be based off of another iamge, either an OS or another image that was created before, based on an OS. All offfical release of operating systems are on Docker Hub.
 ```console
  $ # defines what is the base OS should be for this container. 
  $ # ALL DOCKER FILES MUST START WITH A FROM INSTRUCTION
  FROM Ubuntu 
 ```
The RUN instruction instructs Docker to run a particular command on those base images. 
 ```console
 $ # Docker runs the apt-get update command to fetch the updates packages and installs required dependencies on the image
 RUN apt-get update
 RUN apt-get install python

 RUN pip install flask
 RUN pip install flask-mysq1
 ```
The COPY instruction copies files from the local system onto the Docker image. 
 ```console
 $ # the soruce code of our application is in the current folder, and will be copying it over to the location /opt/source-code inside the Docker image
 COPY . /opt/source-code
 ```
ENTRYPOINT allows us to specify a command that will be run when the image is run as a container. 
 ```console
 $ ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
 ```
<h3>Layered architecture</h3>
When Docker builds the images, its builds these in a layered architecture. Each line of instruction creates a new layer in the Docker image with just the changes from the previous layer. 
