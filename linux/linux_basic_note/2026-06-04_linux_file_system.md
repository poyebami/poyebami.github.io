<h1>Linux File System</h1>

<h3>/bin</h3>
Bin is short for binaries which is another word for programs or applications. It contains most of the programs of the system. The `/bin`  directory has the essential programs that the system requires to operate. This likes `ls` `cat` and other basic functions are store in /bin. 

`SBin` are system binaries that a system administrator would use and that a standard user wouldn't have access to without permission. Both of these folders contain the files that need to be accessible when running in single user mode as opposed to the usual multi-user mode. `Single User Mode` is a special mode that boots you in as a `root user` to allow you do a system repairs and upgrades or testing. 

/bin is used by the system and the system admin to perform maintenance. 
<h3>/boot</h3>
This is where the Linux kernel and boot loader files are kept. It contains everything the OS needs to boot.

<h3>/dev</h3>
The /dev directory is a special directory, since it does not really contain files in the usual sense. Rather, it contains devices that are available to the system. /dev is where your devices live. In Linux, devices are treated like files. For example /dev/fd0 is the first floppy disk drive, /dev/sda is the first hard drive. The partition on that disk `/dev/sda` would be `sda1`, `sda2`, `sda3` and so on. Everything from the webcam, keyboard, mouse, and etc will be in /dev. This is typically an area that applications and drives will access and is rarely something a user should be using. 

<h3>/etc</h3>
/etc is where all the configurations are stored. Configuration that are system-wide such as apt. All of the files in /etc should be text files. Some points of interest are:
 
 /etc/passwd
 The passwd file contains the essential information for each user. This is where user account are defined. DevOps proccesses use these to audit users, manage SSH keys, or configure system-level services accounts. 

 /etc/hostname
 defines the unique names of the server.

 /etc/fstab
 The fstab file contains a table of devices that get mounted when the system boots. This file defines the system's disk drives

 /etc/hosts
 This file lists the netwrok host names and IP addresses that are intrinsically known to the system. 

 /etc/init.d
 This directory contains the scripts that stare varius system services at boot time.

 /etc is the core directory for system-wide configuration files and is often referred to as the "brain" or the control center of the operating system. 

<h3>/lib</h3>
/lib, /lib32, /lib64 are where the libraries are stored. Libraries are files that applications can use to perform varius functions. They are required by the binaries in /bin and /sbin. /lib is critical for system troubleshooting, containerization, and security patching. 

<h3>/media or mnt</h3>
/media or /mnt `mount` are directories where you would find your other mounted drives. It can be a floppy disk, USB stick, external hard drive, network drive or a second hard drive. The /mnt directory is used if you are mounting things manually and to leave the /media directory for the OS to manage. 

<h3>/opt</h3>
/opt is the optional folder which is where manually installed software from venders are located. Some software packages found in repos can also be found in /opt. This is wheere software you've created yourself will be located. Think of it as program files folder in Windows, it keepss software separate from the core operating system. 

<h3>/proc</h3>
It is where pseudo files that contain information about system processes and resources. It does not contain files. There are group of numbered entries in this directory that correspond to all the processes running on the system. There are number of named entries that permit access to the current configuration of the system. Many of these entries can be viewed.
 
/proc/cpuinfo  This entry will tell you what the kernel thinks of the system's CPU.

<h3>/root</h3>
/root is the superuser's home directory. Unlike the other user home folder, it does not contain the typical directories inside and it does not reside in the home directory. You can store files in /root. However, you will need root permission to access it. The location of the root directory ensure that root always has access to its home folder. The root directory is the first or top-most directory in a hierarchy. It can be likened to the trunk of a tree, as the starting point where all the branches originiate from. On of the most commonly uses is storing criticcal maintenance scripts, automation setups, or emergency recovery cron jobs (troubleshooting missing, accidentally deleted, or broken scheduled tasks on the server). 

<h3>/tmp</h3>
/tmp is a directory in which programs can write their temporary files. Temp files are cleared on reboot. It is commonly used for crash recovery. Some programs use it to save temporary, auto-saved versions of files in case that app unexpectedly closes. Software uses /tmp to hold intermadiate data, such as files being extracted from a .zip archive or lage datasets being sorted. Database managers (like MySQL) and text editors use it to create "lock" files to prevent multiple processess from editing the same data simultaneously. 

<h3>/var</h3>
/var directory contains files that change as the system is running. /var contains files and directories that are expected to grow in size.

/var/crash holds information about processess that have crashed. 

/var/log is a directory that contains log files for both the system and applications.  These are updated as the system runs. It'sa good idea to view the files in this directory from time to time, to monitor the health of your system. 

/var/spool is a directory used to hold files that are queued for some process, such as mail messages and print jobs. When a user's mail first arrives on the local system, the message are first stored in /var/spool/mail. 

<h3>/usr</h3>
/usr directory contains a variety of things that support user applications. Any applications installed in /usr are considered non-essential for basic system operation.

/usr/local and its subdirectories are used for the installation of software and other files for use on the local machine. What this really means is that software that is not part of the official distribution (which usually goes in /usr/bin) goes here.

When you find interesting programs to install on your system, they should be installed in one of the /usr/local directories. Most often, the directory of choice is /usr/local/bin.

<h3>/home</h3>
/home is where user keep their personal work. In general, this is the only place users are allowed to write files. In the /home folder, each user have their own folder inside. 
