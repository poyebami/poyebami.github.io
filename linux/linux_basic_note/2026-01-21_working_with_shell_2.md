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
 $ grep second sample.txt
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

STDIN is the standard input steam. It accepts text as its input.
 ```console
  $ cat sample_text.txt   <<--- Standard Input
 This is the file content
 ```

STDOUT is the text output from the command printed 
 ```console
  $ cat sample_text.txt
 This is the file content   <<--- Standard Output
 ```
Error messages from the command are sent through the standard error steam.
 ```console
  $ cat simple_text.txt
 This is the file content
 cat: simple_text.txt : No such file or directory
 ```
With IO redirection, the standard input, output, and error can  be redirected to text files. 

<h3>Redirect STDOUT </h3>
To redirect standout output to a file instead of printing it on the screen, we can use the forward arrow
">" symbol by the name of the file. The forward arrow symbol overwrites the content of the file with the STDOUT
 ```console
  $ echo $SHELL > shell.txt
  $ cat shell.txt
  /bin/bash
 ```
If you want to append STDOUT to an existing fil,e use the double forward arrow ">>" symbol. 
In this case, the string, this is the bash shell, is appended to the existing shell.txt file.
 ```console
 $ echo "This is the Bash shell" >>shell.txt
 $ cat shell.txt
 /bin/bash
  This is the Bash shell
 ```

<h3>Redirect STDERR </h3>
To redirect the error mesage, we need to use the number 3 followed by a foward arrow symbol and the name of the file
in which the errors will be written. If the file doesn't exist, a new one will be created. Otherwise, the file 
will be overwritten.
 ```console
 $ cat missing_file 2> error.txt
 $ cat error.txt
 cat: missing_file: No such file or directory
 ```
To append the standard error to an existing file, use the number 2 double forward symbol.
 ```console
 $ cat missing_file 2>> shell.txt
 $ cat shell.txt
 /bin/bash
 This is the Bash shell
 cat: missing file: No such file or directory
 ```
If you want your command to execute and not print error messages on the screen, even if it generates a standard error, you can redirect to /dev/null
/dev/null is referred to as the bit bucket, the place where you dump anything you don't need, in the case, the standard error, which we do not want to be printed
on the screen. 
```console
 $ cat missing_file 2> /dev/null
```

<h3>Command Line Pipes</h3>
Redirecting date to a file to be later comsumed by another command can be a tedious process. We can overcome this by making use of command line pipes. 
Command line pipes allow the linking of multiple commands. In simple terms, pipes allow the first command's standard out to be used as the standard input
for the second command. The pipes are defined using the vertical bar symbol.
 ```console
 $ cat sample.txt
 hello there!
  Nice to see you here!

 $ grep Hello sample.txt > file.txt

 $ less file.txt
 ```
Making use of the pipe, the output of the command grep hello sample.txt become the standout input for the less command that follows a f ter the operatior.
In this case, the less command will only display the pattern matched by the grep command before the pipe as compared to the entire file.
 ```console
 $ grep Hello sample.txt | less
 Hello There!
  (END) 

 $ less sample.txt
 hello  there!
  Nice to see you here!
  sample.txt (END)
 ```
The differences is that the tee, the standard output is still printed on the screen before overriding the content of the file with the same string. 
 ```console
 $ echo $SHELL |tee shell.txt
 /bin/bash

 $ cat shell.txt
 /bin/bash
 ```
Use tee -a ooption to append the file instead of overriding it. 
 ```console
 $ echo "This is the bash shell"| tee -a shell.txt
 This is the bash shell

 $ cat shell.txt
 /bin/bash
 This is the Bash shell
 ```
