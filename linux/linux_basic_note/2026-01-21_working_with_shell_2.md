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
<h3>Searching for Files and Directories </h3>
 ```console
 $ # print out all paths
 $ locate City.txt
 /home/michael/Africa/Egypt/Cairo/City.txt
 /home/michael/Asia/India/Mumbai/City.txt
 ```
 The depends on a database called mlocate.db for querying the file name. If you just installed linux or if the file you are trying to locate
 was created recently. The command may not yield useful results because the DB has not been updated yet.

 ```console
 $ # update the DB
 $ updatedb
 ```
 The updatedb command need to run as the root user to work.

 ```console
 $ # find files followed by the directory under which you want to search
 $ find /home/michael -name City.txt
 /home/michael/Africa/Egypt/Cairo/City.txt
 /home/michael/Asia/India/Mumbai/City.txt
 ```
<h3>GREP</h3>
To search within files, use the command GREP. GREP is used to print lines of a file matching a pattern.
 ```console
 $ # prints out what is in simple.txt
 $ cat simple.txt
 This is the first line
 Followed bt the second line
 And then the third line
 The fourth line has CAPITAL LETTERS
 The fifth line does not want to be printed
 ```
 ```console
 $ # print out lines matching the search pattern
 $ grep second samiple.txt
 Followed by the second line

 $ # the grep command is also case sensitive
 $ grep capital sample.txt

 $ # search case insensitive
 $ grep -i capital sample.txt
 The fourth line has CAPITAL LETTERS

 $ # search for a pattern recursively within a directory
 $ grep -r "third line" /home/michael
 ./sample.txt: And then the third line. 
 $ # useful when you don't know which file contains the specific pattern that you are looking for
 
 $ # print the lines of a file that don't match a pattern
 $ grep -v "printed" sample.txt
 This is the first line
 Followed by the second line
 And then the third line 
 The fourth line has CAPITAL LETTERS
 ```
Match a pattern that form whole words
 ```console
 $ # print out what is in example.txt
 $ cat examples.txt
 grep examples
 linux exam on 19th
 ```
 ```console
 $ # print out line that contains the pattern "exam"
 $ grep exam examples.txt
 grep "examp"les
 linux "exam" on the 19th
 $ # grep will print out line that contain the pattern "exam" so since examples contains the pattern "exam".
 $ # thus the first line is printed

 $ # to search for just the keyword 
 $ grep -w exam example.txt
 linux exam on 19th 

 $ # print pattern that does not match whole word
 $ grep -vw exam exmaples.txt
 grep examples
 ``` 
 ```console
 $ # print a number of lines after and before matching a pattern

 $ # prints out content on the premier league table.txt file
 1 Arsenal
 2 Liverpool
 3 Chelsea
 4 Manchester City

 $ # using -A1 to print out line matching the pattern and the line below
 $ grep -A1 Arsenal premier-league.table.txt
 1 Arsenal 
 2 Liverpool

 $ # using -B1 to print out line matching the pattern and line above
 $ grep -B1 4 premier-league-table.txt
 3 Chelsea
 4 Manchester City
 $ # if you want nubmer with -A or -B, it will print that number of lines after or before the match
 ```
 ```console
 $ # you can combine both -A and -B
 $ cat premier-league-table.txt
 1 Arsenal
 2 Liverpool
 3 Chelsea
 4 Manchester City
 
 $ grep -A1 -B1 Chelsea premier-league-table.txt
 2 Liverpool
 3 Chelsea
 4 Manchester City
 ```
<h3>IO Redirection </h3>
There are three data streams created when you launch a linux command. 
