<h1>Demo - Advanced Docker Run Features </h1>

<h3>What version of docker image is running</h3>
 ```console
 $ docker run ubuntu cat /etc/*release*
 DISTRIB_ID=Ubuntu
 DISTRIB_RELEASE=24.04
 DISTRIB_CODENAME=noble
 DISTRIB_DESCRIPTION="Ubuntu 24.04.4 LTS"
 PRETTY_NAME="Ubuntu 24.04.4 LTS"
 NAME="Ubuntu"
 VERSION_ID="24.04"
 VERSION="24.04.4 LTS (Noble Numbat)"
 VERSION_CODENAME=noble
 ID=ubuntu
 ID_LIKE=debian
 HOME_URL="https://www.ubuntu.com/"
 SUPPORT_URL="https://help.ubuntu.com/"
 BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
 PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
 UBUNTU_CODENAME=noble
 LOGO=ubuntu-logo
 ```
The version I'm running is 24.04. 

To run any version use the tag `:` and supported tags. 

<h3>Detach and Attached </h3>
To run a docker container in the background or detached mode which out being stuck in the container, run the docker command with `-d`. 
 ```console
 $ docker run -d ubuntu sleep 1500
 f13b85a3e0405...
 ```
Now that you are running the container in detached mode, how do you want to attach back into the container. Run the docker command with `attach` and the `container_id`
 ```console
 $ docker attach f13b85a3e0405
 ```
This will bring you back into the container and its running in the foreground.

<h3>Internal IP in Docker Container</h3>
 ```console
 $ docker inspect <container_id>
 $ docker inspect eb853f3ede72
 ```
The internal IP will be under Network sections.

To enter in Jenkins, use the inspect command to get the internal IP. Also use the ps command to see the port number of Jenkins. After getting all that information, use the `internal IP` followed by the `port number`.
 ```console
 $ # example
 172.17.0.2:8080
 ```
 To save data from a container even after stopping it and without having to start all over. You will have to map it to a directory you want the data to save to.
