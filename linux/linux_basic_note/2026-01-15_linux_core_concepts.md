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

 $ $ closes the directory stream assoicated with dirp
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

  $ # number 8 erfers to a block disk while the minor numbers is used to differentiate amongst devices taht are similar and share the same major number.
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
