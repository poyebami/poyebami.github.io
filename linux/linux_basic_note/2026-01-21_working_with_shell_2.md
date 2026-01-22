<h1>Working with the Shell 2</h1>


<h3>File Compression and Archival </h3>
Checking the size of the file using
 ```console
 $ # checking the size of the file
 $ du -sk test.img
 100000
 ```
 -s : shows only the total size of text.img

 -k : displays the size in kilobytes

 ```console
 $ # prints the size in a human-readable format
 $ du -sh test.img
 98M    test.img   
 ```
 the size of the file is 98MB

 -h : print in human-readable format

 ```console
 $ # prints the size of the file 
 $ ls -lh test.img
 -rw-rw-r-- 1 99M Mar 13 15:48 test.img
 ```
 -l : long listing format

<h3>Archiving File </h3>
Tar (tape archive) is used to group multiple files or directories into a single files and useful for archiving data. Files created with tar are called tarballs.

 ```console
 $ # create and naming an archieve
 $ tar -cf test.tar file1 file2 file3

 $ # display detailed infomraion about file, including its last modification time
 $ ls -ltr test.tar
 -rw-rw-r-- 1281054720 Mar 13 19:48 test.tar
 ```
 -c :create an archieve

 -f : specify the name of that tar file

 ```console
 $ # print the contents of the tarball
 $ tar -tf test.tar
 ./file1
 ./file2
 ./file3

 $ # extract the contents from the tarball
 $ tar -xf test.tar

 $ # compress the tarball to reduce its size
 $ tar -zcf test.tar file1 file2 file3
 ```
<h3>Compression </h3>
Use to reduce the size consumed by a file or a dataset. Three of the popular compression commands:
 ```console
 $ bzip2 test.img
 $ du -sh test.img.bz2
 4.0K   test.img.bz2
 ```
 ```console
 $ gzip test1.img
 $ du -sh test1.img.gz
 100K   test1.img.gz
 ```
 ```console
 $ xz test2.img
 $ du -sh test2.img.xz
 16K    test2.img.xz
 ```
 The size of the compressed file created by these three commands depends on the type of data being compressed, compression algorithm and compression level. 
 The compression command adds a file extension to the file after the operation. 
 
 <h3>Uncompression </h3>
 The compressed file can be uncompressed using the commands below: 
 ```console 
 $ bunzip2 test.img.bz2
 $ du -st test.img
 99M    test.img
 ```
 ```console
 $ gunzip test1.img.gz
 $ du -sh test1.img
 99M    test1.img
 ```
 ```console
 $ unxz test2.img.xz
 $ du -sh test2.img
 99M    test2.img
 ```
However, compressed file does not have to be uncompressed every time. Tool such as zcat, bzcat, and xzcat allow the compressed file to be read without uncompressing them.
 ```console
 $ zcat hostfile.txt.bz2
 127.0.0.1      localhost
 127.0.1.1      Minty-Bionic

 # The following lines are desirable for IPv6
 capable hosts
 ::1        ip6-localhost ip6-loopback
 fe00::0    ip6-localnet
 ff00::0    ip6-mcastprefix
 ff02::1    ip6-allnodes
 ff02::2    ip6-allrouters
 ```
