<h1>Chapter 1: Working with the Shell 1</h1>

<h3>Home Directory</h3>

* `Home Directory` is the home directory for the current user

  ```console
  /home/prosper # this is my home directory
  ~ # tilde represents the home directory and shortcut
  $ cd ~ # this is how you get to the home directory
  $ echo $HOME # echos the path of the home directory 
  ```

<h3>Command and Arguments</h3>

* Arguments act like an input

  ```console
  $ echo "hello world" # hello world is the argument in this command
  $ rm -r <folder_name> # folder name is the argument you are providing to delete a folder and everything in it
  ```

<h3>Commands Type</h3>

* Internal / Built in Command and External Commands
* To determine if a command is internal or external, use type command

  ```console
  $ echo # echo is a shell built-in # echo is a internal command
  $ mv # mv is hashed (/bin/mv) mv is a a external command
  ```

* `Internal` are part of the shell and built in. There are about 30 commands
* Example of Internal Commands are : 
 
  ```console
  $ cd # change directory
  $ export # export environment variable
  $ mkdir # make directory
  $ pwd # print working directory
  ```

* `External` are bingary programs or scripts
* External commands must be installed

<h3>Basic Linux Commands</h3>

  ```console
  $ cat /etc/os-release #identify the ooperation system use

  $ pwd # present working directory

  $ ls  # list content in directory
  $ ls -l # provides more details about the files and directories
  $ ls -a # list all files including hidden
  $ ls -lt # list long files in order created
  $ ls -ltr # long list files in the perverse order created

  $ mkdir # makes new directory / multiple directories
  $ mkdir -p # creates parent directory if it doesn't exist 
  $ mkdir Asia/ # make a directory called Asia

  $ cd # change directory
  $ cd .. # takes you to one directory lower
  $ cd . # keep you in current directory
  $ cd - # takes you to previous directory 
  $ # If I'm in ~/repos/Asia and i moved to ~/Downloads, cd - will take me back to ~/repos/Asia

  $ pushd # change current working directory to directory specified in argument
  $ pushd ~/repos # change working directory to repos

  $ popd # takes you back to previous working directory

  $ mv # moves / rename files or directories
  $ mv ~/Asia/Japans ~/Asia/Japan # rename file
  $ mv ~/Asia/UK ~/Europe/ # move file UK to Europe directory
  $ mv ~/Asia ~/Continents # move Asia directory to Continents directory

  $ cp # copy file
  $ cp -r # copy directories
  $ cp -r ~/Asia ~/Continents # copies Asia directory to continents and there are now 2 Asia directories
  $ cp ~/Asia/Japan ~/Europe/ # copies Japan file from Asia directory

  $ rm # delete files or directory
  $ rm ~/Asia/UK # UK file will be deleted
  $ rm -r ~/Asia #Asia directory will be deleted
  $ rm -f # will force deletion, -rf will force folder deletion

  $ cat # contents in the file will be printed
  $ cat ~Asia/Japan #content in Japan file will be printed

  $ touch # create a new file
  $ touch <file_name> # can create multiple like mkdir

  $ more <file_name> # view text files in a scrollable manner
  $ less <file_name> # view the content of a file and navigate through the file
  
  $ whatis <command> # displays a one-line decription of what a command does
  
  $ man <command> # displays even more detail about command, often with examples and use cases

  $ vi # file editor

  $ clear # clears the visible screen
  ```
  
<h3> Absolute and Relative Path </h3>

* `Absolute Path` is the location of a file or directory starting from the root directory

  ```console
  $ cd /home/prosper/Asia
   ```

* `Relative Path` jumps straight to the directory without writing the whole root directory

  ```console
  $ cd Japan/ # I'm currently in ~/Asia directory, don't need to specific /home/prosper/Asia/Japan/
  ```

<h3> Bash Shell </h3>
There are different types of shell in linux.
 * Bourne Shell (sh)
 * C Shell (csh or tcsh)
 * Korn Shell (ksh)
 * Z Shell (zsh)
 * Bourne again Shell (bash)

```console
 $ # check the shell being used
 $ echo $SHELL
 /bin/bash

 $ # change shell and after log in a new therminal session to see the change
 $ chsh
 Password:
 Changing the login shell for michael
 Enter the new value, or press ENTER for the default
         Login Shell [/bin/bash]: /bin/sh
 ```

<h3> Bash Shell Features </h3>
Bash support command auto-completion. Bash will auto-complete commands if you type part of it and press the Tab Key. In Bash, we can set custom aliases for
the actual commands.

```console
 $ # creating a custom aliases for date command
 $ alias dt=date

 $ # list the perviously run commands
 $ history
 ```

<h3> Bash Envioronment Variables </h3>
  ```console
  $ echo $SHELL
  ```
$SHELL is a environment variable. Variable are used to store information. Environment Variables store infomation about the user's login session.
 ```console
 $ # shows the list of all environment variable
 $ env

 $ # set an environment variable 
 $ export OFFICE=caleston
 $ echo $OFFICE
 caleston
 $ OFFICE=caleston # only apply the variable within the shell. 

 $ # To make these variable persistent over subsequent login or reboots, add them to the .profile or .pam_environment file in the user's home directory.
 $ echo 'export MY_VARIABLE="example_value"' >>~/.profile
 
 $ to add an alias, like ll for ls -1 to profile
 $ echo 'alias ll="ls -1"' >>~/.profile
 ```
When a user issues an exernal command into the shell, the shell uses a PATH variable to search for these external commands.
 ```console
 $ # see the directories defined in the PATH variable
 $ echo $PATH

 $ # check if the location of a commmand can be identified
 $ which obs-studio

 $ # path to this program is not defined in the PATH variable
 $ obs-studio
 obs-studio: command not found

 $ # adds the PATH
 $ export PATH=$PATH:/opt/obs/bin

 $ # the PATH is set and check using the WHICH command again
 $ which obs-studio
 /opt/obs/bin/obs-studio
 ```

<h3> Bash Prompt </h3>
 ```console
 [~]$
 ~ = Presents Working Directory
 $ = User Prompt Symbol

$ #  It can be customized to show the username and the hostname.
$ #  Help when a user is logged into multiple systems trhough multiple terminals.
$ [michael@prod-server]$
 ```
The Bash Shell prompt is set and controlled by a set of speical shell environment variables. 
The most common is PS1 variable.
  ```console
  $ echo $PS1
  [\W]$

  \W = Presents Working Directory =~
  $ = Prompt Symbol
  ```
Customize the prompt by updating the PS1 variable. Bash displays the primpary prompt PS1 when its ready to read a command.
 ```console
 $ PS1="ubuntu-server:"
 ubuntun-server:

 ubuntun-server: echo $PS1
 ubuntun-server:

 ubuntsu-server: PS1="[\d \t \u@\h:\w ] $ "
 [Thu Mar 12 22:12:54 bob@caleston:~ ] $
 ```
