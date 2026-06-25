<h1>File Permissions </h1>

<h3>Cracking the Permission Code</h3>
What does -rwxr-xr-- mean?

The first character in the permission string represents the file type.
 ```console
 - = files  (-rw-rw-rw-) 
 d = directory (drwxrwxr-x)
 l = symlink
 ```
 The next 9 characters are the permssions and who can run them.
 ```console
 2-4 = owner
 5-7 = groups
 7-9 = others
 ```
What does r,w,x mean:
 ```console
 r = read        | Files = can view files contents                  | Dirs: can list directory contents (ls)
 w = write       | Files = can modify or delete files               | Dirs: can create or delete files inside it
 x = execute:    | Files = can run the files as a program / script  | Dirs: can enter the directory (cd)
 ```
```console
$ # example of file permission
-rw-r--r-- 1 mideo 197609 2667 Jun 24 19:28 linux_basic_index.md
$ # the file type is a file. The owner can use read and write permissions but can't execute the file.
$ # the group and others can only read the files but can't not write and execute the file.

drwxr-xr-x 1 mideo 197609    0 Jun 24 19:31 linux_basic_note/
$ # the file type is a directory. The owner has read, write and execute permissions.
$ # the group and other have both read and execute permissions but does not have write permission. 
```
<h3>CHMOD - Changing Permissions</h3>
There are two ways to set permissions: symbolic and numeric.

SYMBOLIC: Used for targeted changes
```console
u = user(owner)
g = group
o = others
a = all
+ = add 
- = remove
= = set exactly
```
```console
$ # gives owner execute permission on script.sh
$ chmod u+x script.sh

$ # removes write permission from group on file.txt
$ chmod g-w file.txt

$ # gives other read permission on config
$ chmod o+r config

$ # gives everyone execute permission on deploy.sh
$ chmod a+x deploy.sh
```
NUMERIC
```console
r = 4
w = 2 
x = 1 
total = will be 7
```
```console
$ # gives owner all permission and gives group and others ONLY read and execute permission
$ chmod 755 scrpit.sh

$ # give owner read and write permission and gives group and others ONLY read permission
$ chmod 644 config.txt

$ # gives ONLY owner read and write permission 
$ chmod 600 id_rsa

$ # COMMON USED PERMISSION
$ # 755= scripts, 644 = files 600 = SSH keys 777 = NEVER NEVER USED THIS 
```
