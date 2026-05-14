<h1>Giving a user access to a server with SSH </h1>

First you have to make sure the user public key inside the authorized keys folder in the server. If there is no authorized keys folder in the server create one.
 ```console
 $ # creating a authorized key folder in the .ssh folder
 prosper@Waifu:~/.ssh$ vi authorized_keys
 ```

<h3>Create a user on the server  </h3>
If the user does not have a user in the server, create one. While in the server, use the sudo command + useradd -m <username>
 ```console
 $ # creating a user in the server
 $ sudo useradd prosper

 $ # create guest with a home directory in the server
 $ -m 
 $ sudo useradd -m guest 

 $ # to check to see if the user is created
 $ cd /home
 $ ls
 prosper guest

 $ # create a password for the user
 $ sudo passwd guest

 $ # delete a user(keep their files)
 $ sudo userdel guest
 $ # verify they've gone
 $ id guest
 No such user
 ```
After creating the user, you need to first swap to the new user using this command
 ```console
 $ # swap using while in the /home directory
 $ sudo -su <user>
 $ sudo -su guest
 ```
After swap the user, you need to add a .ssh directory for them. When someone tries to connect, SSH automatically looks in authorized keys file in .ssh folder for their public key. If that file or folder doesn't exist, SSH has nowhere to check and will deny the connection. 
 ```console
 $ # cd in the guest directory
 $ cd guest
 $ # create a .ssh directory and creae a authorized_keys folder for the user
 $ mkdir .ssh
 $ vi authorized_keys 
 $ # add the user public key in the authorized_keys folder
 ```
After adding the public key into the folder, the user should finally be able to enter the server.

<h3> Change the default shell of a User </h3>
To change the default shell of a user, use the command chsh with sudo command.
 ```console
 $ # -s stands for shell
 $ # -chsh stands for change shell
 sudo chsh -s /bin/bash username
 sudo chsh -s /bln/bash guest
 ```
