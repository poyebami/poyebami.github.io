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
<h3>Output Redirection</h3>
