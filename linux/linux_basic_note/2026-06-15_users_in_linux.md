<h1>Users in Linux</h1>
Everything on Linux runs as a user - even  background services. 

The superuser can do anything and the UID (user identifier) is 0. Anyone or anything operating under UID 0 has unrestircted sysytem privileges and bypasses all standart security checks. You rarely log in as root directly. 
UID 1-999 for reserved for background system/service users, daemons, and system applications (e.g., nginx, mysq1, systemd) so they can run with minimal, islocated permissions. Not really real users/ people.
UID 1000+ are given to real users created on the machine. The first personal user account created during setup almost always starts at UID 1000. Each has a home diretory in /home. 

<h3>Where users live on Disk</h3>
Linux stores user information in plain text files. 
 ```console
$ /etc/passwd - basic user info (readable by everyone)
 ```
 /etc/passwd files is a plain-text database in unix-like operating system that stores essential user account information. It contains one record per line, with each line split into seven colon-separated fields detailing the username, password status, user ID (UID), group ID (GID), user info, home directory, and login shell.
 ```console
$ cat /etc/passwd | grep ubuntu
ubuntu:x:1000:1000:Ubuntu:/home/unbuntu:/bin/bash
nolan:x:1002:1002::/home/nolan:/bin/sh
 ```
Username: the login name used to access the system (between 1 and 32 characters)

Password: typically contains an x, which indicates the actual secure password is stored in the `/ec/shadow` files

User ID (UID): a unique numerical identifier

Group ID (GID): the numerical identifier of the user's primary group

User Info (GECOS): optional comment field, often used to store that user's full name, phone number, or other contact details.

Home Directory: The absolute path to the user's personal directory (e.g., /home/username)

Login Shell: the absolute path to the program that starts automatically when the user logs in (e.g., /bin/bash or /bin/sh)
