<h1>Linux Core Concepts </h1>


<h3>Linux Kernel </h3>
Kernel is the major component of an operating system and is the core interface between a computer's hardware and its processesi.
The Kernal is responsible for four major task. Linux Kernal is monolithic. The kernel carries out CPU sheduling, memory management, and 
several other operations by itself. The kernal is also modular, which means it can extend its capabilities through the use of dynamically 
loaded kernal modules. 

 * Memory Management : keeps track of how much memory is used to sotre what and where
 * Process Mangagement : determines which processess can use the CPU, when, and for how long
 * Device Drivers : acts as a mediator or an interpreter between the hardware and processes
 * System calls and security : receieve requests for service from the processess

<h3>Ways to identify the Linux Kernel version </h3>
 ```console
 $ # display information about the kernel
 $ uname
 Linux

 $ # print the kernel version
 $ uname -r  or uname -a
 4.15.0-72-generic 
 ```
    * 4 = Kernel Version
    * 15 = Major Version
    * 0 = Minor Version
    * 72 = Patch Release
    * Generic = Distro Specific Info

<h3>Memory Management </h3>
Memory is divided into two areas, known as `kernel space` and `user space`.
Kernel Space is the portion of memeory in which the kernel executes and provides its services. Kernel Space has unrestricted access to the hardware and 
strictly reserved for running the kernel code, kernel extensions, and most device drivers.

User Space have access to CPU, Memory, and all processess running outside the kernel space. User programs get access to data by making special request
to the kernel called system calls. The user spaces allows the user to open a file, write to a file, list processess, and defining a variable. 
System Calls allows the user programs to request services from the kernel. Example of system calls are :
 ```console
 $ # request that the kernel opens a file
 $ open()

 $ # request that the kernel closes a file
 $ close()

 $ # returns the pointer to a dirent structure representing the next directory entry in the directory stream pointed by dirp
 $ readdir()

 $ # calculates the length of the string pointed to 
 $ strlen()

 $ # closes the directory stream assoicated with dirp
 $ closedir()
 ```

<h3> Working with Hardware </h3>
We connected a usb disk to the system, a corresponding device driver, which is part of the kernel space, will detect the state change and engerates an event 
called `uevent`. Uevent is sent to the user space device maanger daemon called uDev. The uDev service is then responsible for dynamically creating a device 
node associated with the newly attached drive in the /dev filesystem. The newly attached usb disk should be visible under /dev filesystem. 

Ways to List and get detailed information about hardware
 ```console
  $ # display messages from an area of the kernel called the ring buffer.
  $ dmesg

  $ # redirect the output of dmesg using less or search for specific keywords using grep
  $ dmesg | grep -i usb

  $ # udevadm is a management tool for udev
  $ # udevadm info command queries the udev database for device information
  $ udevadm info --query=path --name=/dev/sda5

  $ # listens to the kernel uevents. it prints the details such as the device path and device name
  $ udevadm monitor

  $ # list information on all PCI devices that are in the system
  $ # PCI devices are Ethernet cards, RAID controllers, video cards, and wireless adapters that directly attach to PCI slots in the motherboard
  $ # PCI is an abbreviation for Peripheral Component Interconnect.
  $ lspci

  $ # list information about block devices. SDA is the physical disk.
  $ # type disk refer ot the whole physical disk
  $ # type partition refers to a reusable disk space carved out of the physical disk
  
  $ lsblk
  NAME                 MAJ:MIN  RM      SIZE  RO  TYPE  MOUNTPOINT
  sda                    8:0     0    119.2G   0  disk
    sda1                 8:1     0      100M   0  part  /boot/efi
    sda2                 8:2     0       16M   0  part
    sda3                 8:3     0     71.5G   0  part
    sda4                 8:4     0        1G   0  part
    sda5                 8:5     0     46.6G   0  part  /  

  $ # number 8 refers to a block disk while the minor numbers is used to differentiate amongst devices taht are similar and share the same major number.
  $ # number 0-5 help identify the different partitions for the disk SDA.

  MAJOR NUMBER          DEVICE TYPES
  1                     RAM
  3                     HARD DISK or CD ROM
  6                     PARALLEL PRINTERS
  8                     SCSI DISK
 ```

 ```console
 $ # display the CPU architecture, # of cores, threads, model, etc
 $ # 32bit cpu address and store 2 to the power of 32 values in its registers
 $ # a registers is a location of the CPU that can be repidly accessed.
 $ # used to load date from memory and carry out arithmetic operations
 $ # 64bit cup address and store 2 to the power of 64 values
 $ # 32bit CPU has a maximum memory of 4GB, whereas for 64bit CPU theroretical limit is 18 exabytes.
 $ # 32bit CPU can only run a 32bit OS and 32bit version of a software.
 $ # each CPU can have muitiple cores and threads per core. 
 $ # Sockets x Cores x Threads = CPUs
 $ lscpu
 ```

 ```console
 $ # list the available memory in the system
 $ # --summary : prints the summary
 $ lsmem --summary
 Memory block size : 128M
 Total online memory : 8G
 Total offline memory: 0B

 $ # shows the total versus used memory in the system
 $ # -m = MB -k = KG -g = GB
 $ free -m

 $ # extract detailed infomration on the entire hardware configuration of the machine
 $ lshw

 $ # there are many commands that require root user privilages to work correctly and run programs as super-user.
 $ # when using sudo, you need to enter password.
 $ # with sudo, you can control which user gets to run commands as the super-user. 
 $ # define which commands they can run, and also replay back commands a user has run with root privilages.
 $ sudo lshw
 ```

<h3>Linux Boot </h3>
Linux boot process can be broken down into four stages.
    * Bios Post
    * Boot Loader (GRUB2)
    * Kernel Initialization
    * INIT Process (systemd)

1. Bios Post : Post stands for Power-On Self-Test. In this stage, BOIS runs a POST test to ensure that the hardware components attached to
the device are functioning correctly.

2. Boot Loader (GRUB2) : After the bios post, the BOIS loads and executes the boot code from the boot device. 
Which is located in teh first sector of the hard disk. In linux, this is located in the /boot file system. The boot loader provides the user with a boot screen,
often with multiple options to boot into. Once the selection is made at boot screen, the boot loader loads the linux kernel into memory, supplies it with some parameters, 
and hands over the control to the kernel. GRUB2 stands for Grand Unified Boot Loader Version 2. 

3. Kernel Initialization: After the selected kernel is loaded into the memory, it is usually decompresssed. This is done as the kernels are in a compressed state to conserve space.
The kernel is then loaded into the memory and starts executing. During this phase, the kernel carries out tasks, such as initializing hardware and memory management tasks, among other
things. Once it is completely operational, the kernel looks for an INIT process to run, which sets up the user sapce and the processess needed for the use environment. 

4. INIT Process: the INIT funcation then calls the systemd daemon. Systemd is responsible for bringing the linux host to a usable state. Systemd is responsible for mounting files systems,
starting, and managaing system services. In the past, another initialization processes called SYSV-INIT (SYS5) was used. It was used in RHEL6 or CentOS 6 distributions. One of the advantages of 
using systemd over sysv-init is that it reduces system startup time by parallelizing the startup of services. To check the INIT system used run
 ```console
  ls -l /sbin/init
  lrwxrwxrwx /sbin/init -> /lib/systemd/systemd
 ```

<h3>Runlevels </h3>
Linux can run in multiple modes. These modes are set by the runlevel. To see the operation mode set in the system, run the command called runlevel in the shell. 
 ```console
 $ runlevel
 N  3
 ```
 Runlevel 5: boots into a graphical interface
 
 Runlevel 3: boots into a command line interface.

During boot, the INIT processess checks the runlevel. It makes sure that all programs needed to get the system ooperational in that mode are started.
For example, the graphical user mode requires a display manager service to run for the GUI (graphical user interface) to work.

In systemd, runlevels are called targets. 
* Runlevel 0: is called poweroff.target
* Runlevel 1: is called rescue.target
* Runlevel 2: is called multi-user target
* Runlevel 3: is called multi-user target
* Runlevel 4: is called multi-user target
* Runlevel 5: is called the graphical target
* Runlevel 6: is called the reboot.target

 ```console
 $ # see default target
 $ systemctl get-default
 graphical.target
 $ # the command looks up the file located at /etc/systemd/system/default.target

 $ ls -ltr /etc/systemd/system/default.target
 /etc/systemd/system/default.target -> /lib/systemd/system/graphical.target

 $ # change the default target
 $ systemctl set-default multi-user.target
 Created symlink /etc/systemd/system/default.target -> /lib/systemd/system/multi-user.target
 ```

<h3>File Types </h3>
There are 3 types of files. Regular files, directory, and speical files. 
 * Regular files hare the most common type of files that contains some text, data, or images. Examples are configuration files, shell scripts or code, JPEG files, etc. 
 * Directory is a type of file that stores other files and directories within. 
 * Special Files can be subcategorized into 5 other file types.
   1. Character files represent devices under the /dev file system that allows the OS to communicate to I/O devices serially. Example includes devices such as the mouse and keyboard.
    
   2. Block files represent devices under /dev. Block device from and write to the device in block, or a chunk of data. Example of block decives are hard disks and RAM.
    
   3. Links in Linux are a way to associate two or more filenames to the same set. There are two types of links.
    `HARD LINK` associates two or more filenames that share the same block of data on the physical disk, although they behave as independent files. Deleting one link will delete the data.
    `SOFT LINK` or symbolic link (symlink) is pretty much a shortcut in Windows. They act as pointers to another file. Deleting a symlink does not affect the data in the actual file.
    
   4. Socket files is a special file that enables the communication between two processes.
    
   5. Named Pipes is a special type of file that allows connecting one process as an input to another. The data flow in a pipe is unidirectional from the first process to the second.

How to identify the different file types in linux
 ```console
 $ file /home/michael/
 /home/michael/: directory

 $ file bash-script.sh
 bash-script.sh: Bourne-Again shell script, UTF-8 Unicode text executable

 $ file insync1000.sock
 insync100.sock: socket

 $file /home/michael/bash-script
 /home/michael/bash-script: symbolic link to /home/sara/bash-script.sh

 $ ls -ld /home/michael/
 drwxr-xr-x 3 root root 4096 Mar 18 17:20 /home/michael/
 $ # from the command output, look at the first character. The letter D denotes that this is a directory

 We can indentify the rest of the file type by checking the first letter in the ls -l outpout.
 Directory              d
 Regular File           -
 Character Device       c
 Link                   l
 Socket File            s
 Pipe                   p
 Block Device           b
 ```
<h3>Filesystem Hierarchy </h3>
 ```console                            
                            /(root Partition)
/bin    /boot   /dev    /etc    /home   /lib    /media  /mnt    /opt    /tmp    /usr    /var
 ```
The /home is the location that contains the home directories for all users, except for the root user.

The root user's home directory is located at /root.

Install any third-party program, put them in the /opt filesystem.

/mnt is used to mount filesystem temporarily in the system. 

/tmp directory is used to store temporary data.
external media such as usb disk will be mounted under /media

 ```console
 $ # df or disk filesystem command prints out details about all the mounted filesystems.
 $ df -hP
 ```
 
/dev filesystem contains the sepcial block and character device files. Contains files for devices such as external 
hard disks, and devices such as the mouse and keyboard. basic programs and binaries such as
the CP, MV, MKDIR, data commands are located in the /bin directory.

/etc is used to store most of the configuration files in linux.

/lib and /lib64 is the place to look for shared libraries to be imported into programs.

/usr used to be the home directories in older systems. Now its the location where all userland applications and their data reside. Examples 
of the applications are the Thunderbird Mail Client, mozilla firefox, and vi editor, etc.

/var is the directory where the system write data such as logs nad cached data. When running into issues with the system or an application, look at the logs in /var
