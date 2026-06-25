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
