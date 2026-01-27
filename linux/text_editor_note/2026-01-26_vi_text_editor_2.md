<h1>VI Editor 2 </h1>
Even though they are different text editor in linux, the most popular one is VI Editor.
The command to open the editor is VI followed by the name of the file you want to create or edit.
 ```console
 $ # open vi editor
 $ vi "filename"
 $ vi /home/micheal/sample.txt
 ```
<h3>Command Mode </h3>
In command mode, press "yy" to copy a line.
 
To paste, just press "p".

To save the file, you uppercase "ZZ".

To delete a letter, press "x".

To delete a line, press "dd".

To delete three line from the current line, press "d3d" or 3dd. Replace the 3 with any number to delete
that many lines from the current line. 

To undo the previous change, press "u". 

To redo the change again, press "Ctrl-R".

To find a string. use either "/" or "?" followed by the pattern.
"/" searches the file from the current line downward until it finds the matches. This will find the first occurrence down the file, to find the next 
occurrence down the file press "n". To find the pattern above the current line, press "N".

"?" does the same thing but in reverse. It searches for the pattern f rom the cursor and moves upwards to find the next match. 
Use "n" will move to find the next match and "N" searches down the file. 

<h3>Insert Mode</h3>
i : insert the text before the current cursor position

a: appends text after the current cursor position.

o: opens a new line below the current line and palces the cursor at the beginning of that new line in insert mode.

I: inserts text at the beginning of the current line, regardless of the cursor's starting position.

A: appends text to the end of the current line, regardless of the cursor's starting position.

O: opens a new line above the current line and places the cursor at the beginning of that new line in insert mode.

<h3>Lastline mode </h3>
:w - saves the file after making a change but will still be within the editor.

:q - to exit the file

:wq - to save and exit the file

:q! - to quit without saving the file.

<h3>VIM</h3>
VIM (VI Improved) is another popualar text editor but it is a improved version of VI with added features.
The VI is a symbolic link or a shortcut to the VIM editor. To see the differences between VI and VIM, 
use the man pages or check within VIM. 

To open a file using VIM:

type VIM "filename" to see the differences use :hvi- differences
