<h1>Storage Basic </h1>
Block Device is a type of file that can be found under the /dev directory. It usually represents a piece of hardware that can store data. Hard Disk and SSD (soild-state disk) are example of block storage in Linux. It is called
block storage because data is read or written to it in blocks or chunks of space. To see the list of block devices in the system, run this command...
 ```console
 $ lsblk
 NAME           MAJ:MIN     RM      SIZE    RO      TYPE    MOUNTPOINT
 sda              8:0       0    119.2G     0       disk
  sda1            8:1       0     100M      0       part    /boot/efi
  sda2            8:2       0     72.5G     0       part    /media/MM/Data
  sda3            8:3       0     46.6G     0       part    /
 ```
 or run this command
 ```console
 $ ls -l /dev/ | grep "^b"
 brw-rw---- 1 root disk     8,      0 Mar 19 17:43 sda
 brw-rw---- 1 root disk     8,      1 Mar 19 17:43 sda1
 brw-rw---- 1 root disk     8,      2 Mar 19 17:43 sda2
 brw-rw---- 1 root disk     8,      3 Mar 19 17:43 sda3
 ```
Using the lsblk command, you can see there is sda with 119.2G. This represents an entire disk. Then there are devices SDA1 to SDA3, which are of the type part. Those are disk partitions. 
 
Each block device has a major and a minor number 
The `major numbers`, which is the number 8 in the example above, is used to identify the type of block device. The value 8 represents a SCSL device, which has a fixed naming convention that starts with SD. This is the re ason why the disk andthe partitions names
starts with SD. 
 ```console
 Major Number           Device Type
 1                      RAM 
 3                      HARD DISK or DC ROM
 6                      PARALLEL PRINTERS
 8                      SCSI DISK
 ```
 SCSI Device (small computer system interface) is a high-performance hardware peripheral- such as a hard drives, tape drives, or scanners- that connects to a computer using a specialized parallel or serial interface. 
The `minor numbers` are used to distinguish individual physical or logical devices, which in this case identify the whole disk and the partitions created. 

<h3>DISK PARTITIONS</h3>
The entire disk can be broken down into smaller segments of usable space called partitions. In the example above, there are three partitions for the SSD disk. (SDA1, SDA2, SDA3). The concept of partitioning allows us to segment space and use each partition for a specific purpose.
 ```console
  $ lsblk
  NAME           MAJ:MIN     RM      SIZE    RO      TYPE    MOUNTPOINT
  sda              8:0       0    119.2G     0       disk
   sda1            8:1       0     100M      0       part    /boot/efi
   sda2            8:2       0     72.5G     0       part    /media/MM/Data
   sda3            8:3       0     46.6G     0       part    /
  ```
  Looking at sda3 partition, we can see that it is used for the root partition. SDA2 partition with 72.5GB is mounted at /media/mm/data, which is used to store backups in this system. SDA1 is used as a system partition mounted at /boot/EFI, which is used during the system boot process and contains the boot loaders for the installed OS. 

Another way to see partition information is use the fdisk command.
 ```console
 $ sudo fdisk -l /dev/sda
 Disk /dev/sda: 119.2 Gib, 128035676160 bytes, 250069780 sectors
 Units: sectors of 1 * 512 = 512 bytes
 Sector size (logical/physical): 512 bytes / 512  bytes
 I/O size (minimum/optimal): 512 bytes / 512 bytes
 Disklabel type : gpt
 Disk identifier: 72ABF26E-9723-4406-ZEA1-C2B9B6270A23

 Device         Start       End         Source      Size    Type
 /dev/sda1      2048     206847         204800      100M    EFI System
 /dev/sda2    239616  150194175      149954560     71.5G    Linux filesystem
 /dev/sda3 150194176  247955455       97761280     46.6G    Linux filesystem
 ```

<h3>Partition Types </h3>
There are three types of disk partitions. 

The `primary partition` is a type of partition that can be used to boot an operation system. Traditionally, disk were limited to not more than four primary partitions per disk. 

An `extended partiton` is a type of partition that cannot be used on its own, but can host logical partitions. With the restrictions of a maximum of four primary partitions, you can opt to create extended partitions and carve out logical partitions inside of it. 
Extended partition is like a disk drive in its own right. It has a partition talbe that points to one or more logical partitions.

`Logical partition` are those created within an extended partition. 

How a disk is partitioned is defined by a partitioning scheme, also known as a partition table. 

MBR partitioning scheme (Master Boot Record) is a legacy partition style supporting drives up to 2TB and a maximum of four primary partitions. It works with older BIOS-based system, ideal for older hardware or 32 bit systems. 
If you want more than four partitions per disk, we would need to create the fourth partition as an extended partition and carve out logical partition within it. 

GPT (GUID Partition Table) is a more recent partitioning scheme that was created to address the limitations iN MBR. GPT can have unlimited number of partitions and restrictions imposed by the operating system. For example, RHEL (RED HAT ENTERPRISE LINUX) only allows 128 partitions per disk. 

<h3>Creating Partitions </h3>
To create partition on a disk, run this command
 ```console
 $ gdisk /dev/sdb
 GPT fdisk (gdisk) version 1.0.1

 Partition table scan:
    MBR : protective 
    BSD : not present
    APM : not present
    GPT : present

Found valid GPT with protective MBR; using GPT

Command (? for help):
 ``` 
 ```console
 $ # commands in ? 

 b: back up   GPT data to a file
 c: change a partition's name
 d: delete a partition
 i: show detailed information on a partition
 l: list know partition types
 n: add new partition
 o: create a new empty GUID partition table (GPT)
 p: print the partition table
 q: quit without saving changes
 r: recovery and transformation option (expects only)
 s: sort partitions
 t: change a partition's type code
 v: verify disk
 w: write table to disk and exit
 x: extra functionality (expects only)
 ?: prints this menu
 ```
Gdisk is an improved version of the Fdisk that works with the GPT partition table. 

1. To create a new partition, we need to enter `n`. We create a partition number `1` with the size of `20` GB.
2. After entering the partition size, it will ask for the hex code for the partition type. In our case, we will stick to the default of Linux filesystem, which has a code of 8300. 
3. You can now type in the L key to see all possible values. 
4. Once you provide the necessary information, use the W command to write the partition table. This will create a new partition called /dev/sdb1. 
5. Check the status of the new partition, run the lsblk or fdisk -l command. You can see the partition table using the gdisk -l command as well. 
