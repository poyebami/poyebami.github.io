<h1>Bash Script</h1>
<h3>Creating bash script</h3>
When creating a bash script, make sure to put `.sh` at the end of the new file. .sh file is a shell script used to automate commands in linux. 
 ```console
 $ # use .sh to make a shell script
 touch script.sh
 ```
<h3>Running a bash script</h3>
After writing your script. Save and quit out of the file and run 
 ```console
 $ # running a bash script
 $ bash script.sh
 $ # output: hello world!
 ```
We should always provide an interpreter for our shell scripts to use the correct type of shell such Bash, bourne shell, z shell, and kornshell. It make it easier for us, we can put the interpreter at the top of our shell script.
 ```console
 $ # /bin/bash bash is our interpreter
 #!/bin/bash 
 echo hello world
 ```
We are using shebang (#!) to tell the shell script which interpreter to use and follow by the full path of the interpreter. Instead of running bash script.sh to run the script, we use `./`to run the script.
 ```console
 $ ./script.sh
 $ # output: bash: ./script.sh: Permission denied
 ```
We see that we don't have the permission to run the script. I run ls -la to see the permission
 ```console
 $ # list the permission for the owner, group, and others
 $ ls -la
 $ # output: -rw-rw-r-- 1 prosper prosper 19 Jul 14 21:11 script.sh
 ```
As the owner, we don't have execute permission. To give execute permission run: 
 ```console
 $ # give roles permissions
 $ chmod u+x script.sh
 $ ls -la 
 $ # output: -rwx-rw-r--
 ```
 We now have permission to run script.sh
 ```console
 $ # after giving user permission to execute the file
 $ ./script.sh
 $ # output: hello world
 ```
