<h1>Output/Input Redirection</h1>

<h3>Piping</h3>
Piping is a form of redirection (transfer of standard output to some other destination) that is used in linux to send the output of one command, program, process to another command , program and process for further processing. The piple character is `|`.

<h3>Example of Piping</h3>
Piping can be used to filter out certain files or subdirectories.
 ```console
 $ # use the | and grep to find file.txt
 ls -la | grep file.txt

 $ # output: file.txt
 $ # result is a list of files that match the search term.
 ```
 ```console
 $ # another way to grep in different directories 
 $ # prints out files that match bash in /usr/bin
 ls -la /usr/bin/ | grep bash
 
 $ # output: -rwxr-xr-x  1 root root     1396520 Mar 14  2024 bash
 $ # output: -rwxr-xr-x  1 root root        6818 Mar 14  2024 bashbug
 $ # output: -rwxr-xr-x  1 root root        4414 Nov 11  2021 dh_bash-completion
 $ # output: lrwxrwxrwx  1 root root           4 Mar 14  2024 rbash -> bash
 ```
<h3>(>) Output Redirection</h3> 
`>` and `>>` is used to send the output from a command to a file. It can be used for logging to a logfile (for ex. using timestamps) and dynamically creating (config) files.
 ```console
 $ # prints Hello world into a file called hello.txt
 $ # it also creates the file too
 echo Hello world! > hello.txt

 cat hello.txt
 $ # output: Hello world!
 ```
Right now hello.txt has the "Hello world!" written in the file. But what happens if we use the same command but with different text
 ```console
 echo Good day to you! > hello.txt

 cat hello.txt
 $ # output: Good day to you!
 ```
 We see that the file has been overwritten. It no longer print "Hello World!" but only "Good day to you!" The `>` always overwrites an existing file. 

<h3>(>>)Output Redirection</h3>
`>>` will append any output to our destination file rather than overwrite it.
 ```console
 $ # hello.txt now has Hello world!

 $ # to append the output use >>
 echo Good day to you! >> Hello.txt
 cat Hello.txt
 $ # output: Hello world!
 $ # output: Good day to you!
 ```
In real world application, we use this with timestamps to see which command ran at which time and also gather some errors. 

<h3>Input</h3>
`<` is used to get input from a txt file. 
 ```console
 wc -w hello.txt
 6 hello.txt
 
 $ # `<` redirect the content of hello.txt into wc's standard input.
 $ # wc never see thge filename
 wc -w < hello.txt
 6 
 ```
<h3>Input Part2</h3>
`<<` is a heredoc (here document). Compare to `<` which redirect file's contents into a command, it lets you type multi-line input directly in your script/ terminal, ending when delimiter word is seen.
 ```console
 cat << EOF
 > I will
 > write some
 > text
 EOF

 $ # output: I will
 $ # output: write some
 $ # output: text
 ```
<h3>Input Part3</h3>
`<<<` is called herestring. It feeds a single string directly into a command's stdin.
 ```console
 wc - w <<< "Hello there wordcount!"
 $ # output: 3
 ```
<h3>Combining</h3>
We can write multi-line text into a file, without a text editor.
Below we typing multi-line directly from our terminal without going into the text editor.
 ```console
 cat << EOF > hello.txt
 >Hello there!
 >This is a test file.
 >EOF

 cat hello.txt
 $ # output: Hello there!
 $ # output: This is a test file.
 ```
