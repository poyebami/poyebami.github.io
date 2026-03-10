<h1>File Systems in Linux </h1>
Partitioning alone does not make a disk usable in the OS. The disks and the partitions are seen by the Linux kernel as a raw disk. To write to a disk or a partition, we must create a filesystem. 

`Filesystem` defines how data is stored on a disk. After creating a filesystem, we must mount it to a directory, and that's when we can read or write data to it. 

<h3>Commonly used file system </h3>
 ```console
 EXT2

 2TB File size
 4TB Volume size
 Supports Compression
 Supports Linux Permissions
 Long Crash Recovery
 ```
 ```console
 EXT3

 2TB File size
 4TB Volume size
 Uses Journal
 Backwards Compatible
 ```
The significant difference between the two is that in EXT2, in case of an unclean shutdown, can take quite some time for the system to boot back up. EXT3 filesystem does not have this drawback becasue it has additional features that allowed quicker startup after an unclearn shutdown. 

EXT4 further improves the EXT3 filesystem and is still one of the most common general-purpose filesystems used today.
 ```console
 EXT4

 16TB File size
 1 Exabyte
 Uses Journal
 Uses chksum for Journal
 Backwards Compatible
 ```
A EXT4 filesystem can be mounted as an EXT3 or EXT2 filesystem. Similarly, an EXT3 can be mounted as EXT2. 

<h3>Creating Filesystem</h3>
Using /dev/sdb disk to create an EXT4 filesystem. To start run the mkfs.ext4 command
 ```console
 $ mkfs.ext4 "device_path"
 $ mkfs.ext4 /dev/sdb1

 Allocating group tables: done
 Writing inode tables: done
 Creating journal (32768 blocks): done
 Writing superblocks and filesystem accouting information: done
 ```
The filesystem can be mounted on the system using the mount command
 ```console
  $ mkdir /mnt/ext4;
  $ mount /dev/sdb1 /mnt/ext4
 ```
We can check if the filesystem is mounted by either using the df command or using the mount command again.
 ```console
 $ mount | grep /dev/sdb1
 /dev/sdb1 on /mnt/ext4 type ext4 (rw,relatime,data=ordered)
 ```
 ```console
 $ df -hP | grep /dev/sdb1
 /dev/sdb1      20G       52K     20G     0%      /mnt/ext4
 ```
To make the mount be available after the system reboots, add an entry to the /etc/fstab file.
 ```console
 $ sudo nano /etc/fstab
 /etc/fstab
 # <file system>  <mount point>    <type>       <options>                       <dump>          <pass>
 /dev/sda1             /            ext4         default,relatime,errors=panic    0               1 ~
 
 $ echo " /dev/sdb1 /mnt/ext4 ext4 rw 0 0" >> /etc/fstab
 ```
Nano is a command-line text editor widely used for quick edits to configuration files or short scripts.

```console
FLELD           PURPOSE
Filesystem      Such as /dev/vdb1 to be mounted
Mountpoint      Directory to be mounted on
Type            Example ext2, ext3, ext4
Options         Such as RW = Read-write, RO= Read Only
Dump            0 = Ignore, 1 = take backup
Pass            0 = Ingore, 1 or 2 = FSCK filesystem check enforced
```
The first O indicates whether to back up the file system using a dump utility. It can have two possible values,
zero for disabling backup and one for taking the backup. 

The second O is the priority set for the filesystem check tool to determine the order in which the filesystems should be checked during a boot after a crash. A value of 0 means that tool will ignore the filesystem check. 
1 is usually set for the root filesystem. 2 is used for all other filesystem (checked second, or in parallel with other '2' entries).
