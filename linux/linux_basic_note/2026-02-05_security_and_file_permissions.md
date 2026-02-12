<h1>Security and File Permissions</h1>
There are many ways to secure the linux operating system.

`Access Control` methods make use of the user and password-based authentication to determine who can access the system. 

`PAM` (Pluggable Authentication Module) manages authentication in linux. It used to authenticate users to programs and services in linux.

`Network Security` is used to restrict or allow access to services listening on the linux server. Through we can use external firewall, it can also be 
set up within the linux system by making use of tools such as iptables and Firewalld.

`SSH (Secure Shell)` is used for remote access to a server over an unsecured network. `SSH Hardening` can help make sure only the authorized users gain 
access to the server.

`SELinux` makes use of security policies for isolating applications running on the same system from each other to project the linux server.

<h3>Linux Accounts</h3>
Every user in linux has a associated account. The `user account` maintains information such as the username and password. A user account also has an unique identifier called
UID (user ID). The information about the user account is found in /etc/passwd file
 ```console
 $ cat /etc/passwd
 ...
 ...
 ...
 bob:1000:1000:Bob Kingsley,,,:/home/bob:/bin/bash
 ```
A linux group is a collection of users. It is used to organized users based on common attributes such as role or a function. The information about groups is stored in /etc/group file. Each
group has a unique identifier called a GID.
 ```console
 $ cat /etc/group
 ...
 ...
 ...
 bob:x:1000:
 developers:x:1003:bob;michael
 ```
Each user has a unique username, UID, and GID assigned to them. A user can be part of muitiple groups. If no group is specified when the user is created, it assigns the user to a group with the same ID
and name as the username. That's the primary GID of the user. User account also stores information about the home directory of the user (/home/user) and the default shell(/bin/sh). You can check this
by running the ID command followed by the usrename.
 ```console
 $ id "user"
 $ id michael
 uid=1001(michael) gid=1001(michael)groups=1001(michael), 1003(developers)
 
 $ # check the home directory path and the default shell assigned to the user
 $ grep -i michael /etc/passwd
 michael:x:1001:1001::/home/michael:/bin/sh
 ```
<h3>Account Types</h3>
`User Account` is individual people who need access to the linux system.

A `Superuser Account` is the root, which has the UID zero. The superuser has unrestircted access to and control over the system, including other users.

`System Account` are usually created during the OS installation and for use by software and services that will not run as teh superuser. The UID is usually under 100 or
between 500 and 1000. They usually do not have a dedicated home directory. If they do the home directory is not created under /home. SSHD and the mail user are exaomple of the 
system account. 

`Service Account` are similar to system account and are created when services are installed in linux. NGINX service makes use of a service account called NGINX. 
 ```console
 $ # see the list of users currently logged into the system
 $ who
 bob        pts/2       Apr 28 06:48  (172.16.238.187)

 $ # displays the record of all logged-in users.
 $ last
 michael        :1  :1                       Tue May 12 20:00 still logged in
 sarah          :1  :1                       Tue May 12 12:00 still running
 reboot        system boot 5.3.0-758-gen     Mon May 11 13:00 - 19:00 (06:00)
 ```
<h3>Switching User</h3>
 ```console
 $ # switching users
 $ su -
  Password:
root ~#

 $ # switching users and run a specific command
 $ su -c "whoami"
  Password:
 root 

 $ # however using su need the password of the user you are switching to

 $ # switching user using sudo
 $ sudo apt-get install nginx
 [sudo] password for michael:
 $ # sudo is found under /etc/sudoers files
 
 $ # the sudo files defines the policies applied by the sudo command
 $ # can be updated using the visduo command
 $ cat /etc/sudoers
 User privilege specificiation
 root   ALL=(ALL:ALL) ALL
 # Members of the admin group may gain root privileges
 %admin     ALL=(ALL) ALL
 # Allow members of group sudo to execute any command
 %sudo      ALL=(ALL:ALL) ALL
 # Allow Bob to run any command
 bob  ALL=(ALL:ALL) ALL                     
 # Allow Sarah to reboot the system
 sarah localhost=/user/bin/shutdown -r now
 # See sudoers(5) for more infromation on "#include"
 directives:
 #includedir /etc/sudoers.d
 ```
Only users listed in the /etc/sudoers file can make use of the sudo command for privilege escalation.
It is a added security measure that prevents other users from running commands as the root user.

 ```console
 $ # eliminate the need for ever logging in as the root user with sudo enabled
 $ # setting a no-login shell for the root user 
 $ grep -i ^root /etc/passwd
 /root:x:0:0:root:/root:/usr/sbin/nologin
 ```
<h3>Sudo</h3>
 ```console
 $ cat /etc/sudoers

 $ # the first field is either the user or the group to which privilages have been granted
 $ # groups begin with a % 

 $ # the second field, which by default is left to the value ALL
 $ # specifies the host in which the user can make use of privilage escalation
 $ # in a normal set up, there is only one host, which is the local host and as a result, the value ALL implies the localhost as well

 $ # the third field, enclosed in brackets, implies the users and groups the user in the first field can run the command as
 $ # normal left to the default value of ALL
 $ # implies that any user, not just root, can be used to run the commands

 $ # the fourth field is the command that can be run. 
 $ # you can specify ALL, which means the user can run any command without  restriction
 $ # or specify individual commands, such as the shutdown -r now as in the case of the user called Sarah
 $ # it means that Sarah can only use sudo to reboot the system and nothing else


 1.     User or Group       bob, %sudo (grup)
 2.     Host                localhost, ALL(default)
 3.     User                ALL(default)
 4.     Command             /bin/ls, ALL(unrestricted)
 ```

<h3>Access Cotnrol Files</h3>

