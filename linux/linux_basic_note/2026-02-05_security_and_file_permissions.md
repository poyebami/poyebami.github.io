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
Most of the access control files in linux are stored under the /etc directory. Only the root user has access to write to it. The access control 
files are designed in a way that they should never be modified using a text editor. 

Basic access control files in linux
 ```console
 /etc/passwd does not save any passwords
 $ grep -i ^bob /etc/passwd
 /bob:x:1001:1001::/home/bob:/bin/bash

 /etc/shadow stores passwords and its is hashed
 $ grep -i ^bob /etc/shadow
 /bob:$6$0h0utot0$5JcuRxR7y72LLQk4Kdog7u09
 YcWF/7....

 /etc/group sores information about all user groups 
 $ # such as group name, GID, and memebers
 $ grep -i ^bob /etc/group
 developer:x:1001:bob,michael
 ```
In these files, each line represents information about a particular user or a group
 ```console
 /etc/passwd
 $ grep -i ^bob /etc/passwd
 bob:x:1001:1001::/home/bob:/bin/bash
 USERNAME:PASSWORD:UID:GID:GECOS:HOMEDIR:SHELL
 
 $ # the password field is x because it is store in /etc/shadow file
 
 $ # Geckos is a CSV format, or a comma-separated list of user information 
 $ # such as name, locatio, phone number, etc
 
 $ # Geckos is optional and can be blank
 ```

 ```console
 /etc shadow
 $ grep -i ^bob /etc/shadow
 /bob:$6$0h0utot0$5JcuRxR7y72LLQk4Kdog7u09
 YcWF/7...
 USERNAME::PASSWORD:LASTCHANGE:MINAGE:MAXAGE:WARN:INACTIVE:EXPDATE

 $ # password, contrained the encrypted password. "hashed"
 
 $ # * or empty field implies that password was never set for this user
 
 $ # last change is in epoch, number of seconds that has elapsed since midnight, January 1, 1970
 
 $ # warn is number of days before a password is going to expire that the user 
 $ # should be warned so that they can change the password
 
 $ # inactive is the number of days after a password has expired that it should still be accepted
 
 $ # before being disabled

 $ # expdate is the date when the account will be expired 
 ```

 ```console
 /etc/group
 $ grep -i ^bob /etc/group
 developer:x:1001:bob,michael
 NAME:PASSWORD:GID:MEMBERS
 ```

<h3>User Management </h3>
Commands used to create and manage user accounts in linux

 ```console
 $ # used by system admins to create a new local user 
 $ useradd bob

 $ # set the password for the user
 $ passwd bob
 Changing password for user bob.
 New UNIX password:
 Retype new UNIX password:
 passwd: all authentication tokens updated
 successfully.

 $ # both these commands need to be run as root
 
 $ # once logged in, user can check the user ID
 $ whoami
 bob

 $ # change their own password from the shell. no arguments
 $ passwd
 Changing password for bob.
 (current) UNIX password:
 Enter new UNIX password:
 Retype new UNIX password:
 passwd: password updated successfully
 ```
Using the useradd with options
 ```console
 $ useradd -u 1009 -g 1009 -d /home/robert -s /bin/bash -c "Mercury Project member" bob 

 -c : custom commands
 -d : custom home directory
 -e : expiry date
 -g : specific GID
 -G : create user with multiple secondary groups
 -s : specify login shells
 -u : specific UID

 we can use the id command to validate that the custom fields were set
 
 we can also verify the custom comments have been created by inspecting
 the password file and checking the fields for user's account
 $ grep -i bob /etc/passwd
 bob:x:1009:1009:Mercury Project Member: /home/robert: /bin/bash
 ```
 ```console
 $ # delete a user account
 $ userdel bob

 $ # add a new linux group
 $ groupadd -g 1011 developer

 $ # delete group 
 $ groupdel devloper
 ```
<h3>Linux File Permission</h3>
The first letter of the first colume in the listing from an ls -l command indicates the file types
 ```console
 $ ls -l bash-script.sh
 -rwxrwxr -x 1 bob bob 89 Mar 17 01:35 bash-script.sh
 ```
In this case, the "-" implies the file called bash-script.sh is a file.
 ```console
  File Type                    Identifier
  Directory                    d
  Regular File                 -
  Character Device             c
  Link                         |
  Socket File                  s
  Pipe                         p
  Block Device                 b
 ```
What does the other characters such as rwx in the first column mean? 
 ```console
 $ ls -l bash-script.sh
 -rwxrwxr -x 1 bob bob 89 Mar 17 01:35 bash-script.sh
 ```
These characters describle the file permissions in linux. They can be broken down as the owner permssions, group permissions, and permissions for others.

The first three characters after the file identifers are the permissions for the owner of the file, denoted by the letter u. 
 ```console
 -rwx
 ```
The next three characters are permissions of the group owning the file, denoted by a g.
 ```console
 rwx
 ```
The last three characters are the permissions for all other users, denoted by o.
 ```console
 r-x
 ```
When a r bit is set, the respective user has read permissions to the file. It has the octal value of 4.

When a w bit is set, they have write permissions to the file, with an octal value of 2.

When a x bit i set, the user has the execute permissions for the file, which has an octal value of 1. 

```console
 BIT                PURPOSE                 OCTAL VALUE
 r                  Read                    4
 w                  Write                   2
 x                  Execute                 1
```
<h3>Directory Permissions </h3>
With directories, the same set of permissions that we saw for the file are still applicable. 
```console                                                                                                                                                                                                                                                                                                              
 BIT                PURPOSE                 OCTAL VALUE                                                                                                                                                                                                                                                                 
 r                  Read                    4                                                                                                                                                                                                                                                                           
 w                  Write                   2                                                                                                                                                                                                                                                                           
 x                  Execute                 1
 -                  No permission           0
```
R bit allows the user to read the contents of the directory. 

W bit allows the user to write operation in the directory.

For example: the directory is owned by Bob, the owner has only the execute permission.
``` console
 $ ls -ld /home/bob/random_dir
 d--xrwxrwx 1 bob bob 89 Mar 17 01:35
 $ # here --x means that bob only has the execute permissions. 
```
If Bob tires to list the content of the directory, he will get a permission denied error.
```console
 $ ls /home/bob/random_dir
 ls: cannnot open directory 'random_dir/': Permission denied
```
<h3>Octal Value</h3>
Despite being the owner of the directory, Bob does not have the read access to it . (--x)
All other users have full access to this directory, because they have the read, write, and execute bits set for them (rwx)
Bob can 'cd' into the directory, since the directory has the x bit set for the owner (--x).
However, Bob is part of the group called Bob, that has full acces to the directory.

He doen't have access to them because in linux, the system identifies the user trying to access the file or direcotry and checks the permission sequentially. (following the logical order or sequence)
If the user trying to access is the owner, the owner's permissions for the file are applied, and the rest is ignored. (-xxrwxrwx). In this case (--x) is the first three characters and is meant for the owner.
If the user is not the owner but part of the group, only the group permissions are applied. The others are ignored. (--xrwxrwx). In this case (rwx) is the next three characters and is meant of the group.
Octal value (base-8 numbers) are primarily used as a shorthand, numeric representation for managing file permissions. 
Calculating octal value by adding the values of the granted permissions. 
* rwx (read, write,execute) = 4+2+1=7
* rw- (read, write, no execute) = 4+2+0=6
* r-x (read, no write, execute) = 4+0+1 = 5
* r-- (read only) = 4+0+0=4
* --- (no permissions) = 0+0+0=0

A standard, three-digit octual value is sued to specify permissions for three different user classes in order:
* Owner (user)
* Group
* Others (Everyone else)
 
 ```console
  octal value 755 means:

  Owner : 7  (rwx) = full permissions
  Group : 5  (r-x) = read and execute
  Other : 5  (r-x) = read and execute
 ```
<h3>Modifying File Permissions</h3>
The command used to modify the permissions of a file is called chmod. The syntax to use this command is chmod, followed by permission and finally the filename.
 ```console
 $ chmod <permission> filename
 ```
 Permissions can be modified in two ways, symbolic mode and numeric mode. 

<h4>Symbolic Mode</h4>
In symbolic mode, the first characters following the chmode command specify whose permission you want to alter. 
 ```console
 $ # provide full access to Owners
 $ chmod u+rwx test-file

 $ # provide Read access to owners, group, and others, remove execute access
 $ chmod ugo+r-x test-file

 $ # removes all access to others
 $ chmod o-rwx test-file

 $ # provides full access to owner, add read, remove execute for group and no access for others
 $ chmod u+rwx, g+r-x, o-rwx test-file
 ```
After the characters, you need to specify if you want to grant access with the "+" symbol or revoke existing access with the "-" symbol.

<h4>Numeric Mode</h4>
In numeric mode, we can specify the permissions to be updates in terms of the three-digit octal values. 
 ```console
 $ # provide full access to owners, group, and others 
 $ chmod 777 test-file

 $ # provide read and execute access for owners, group, and others
 $ chmod 555 test-file

 $ # provide read and write access for owners and group, and no access for others
 $ chmod 660 test-file
 
 $ # provide full access for owners, read and execute for group, and no access for others
 $ chmod 750 test-file
 ```
<h4>Changing ownership and group</h4>
To change the ownership and group we must use the chown command. The syntax is chown, followed by the new owner, and group, separated by a colon, and finally the file or directory.
 ```console
 $ chown owner: group file

 $ # changing the owner to bob and group to developer
 $ chown bob:developer test-file

 $ # changes just the owner of the file to Bob. Group unchanged
 $ chown bob andoid.apk

 $ # change the group for the test-file to the group called android
 $ chgrp android test-file
 ```
