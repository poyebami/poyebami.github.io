<h1>Understanding GIT </h1>
GIT is a key value store. When we add a file to commit, the contents of the file are hased using the SHA-1 algorithm. The hash is used as a key name for the folder,
and stores the file using that key name. Git has `Porcelain` and `Plumbing` Commands.

<h3>Porcelain Commands </h3>
 ```console
 $ git add
 $ git status
 $ git commit
 $ git stash
 ```

<h3>Plumbing Commands </h3>
 ```console
 $ # can create the hash ourselves
 $ git hash-object
 $ git ls-files
 $ git rev-parse
 $ git ls-remote

 $ git hash-object first_story.txt
 bea8d7fee87b11c2235ca623935e6ccccd8bac3
 ```
The first two cahracter of the hash above (be) are used as the key. It is the name of the folder that stores the contents of the file, the value.
Git creates a folder called "be." This is visible when you open the .git folder, which gets created when you run git init. When you access the folder, the value of the 
hash is stored in here.
```console
 $ # if we commit the file, the same hassh is created.
 $ git add first_story.txt
 $ git commit -m "First story"
 $ ls ./.git/objects
   26   be  a0  info    pack
 $ ls ./.git/ojects/be
   a87fee8e7b11c2235ca623935e6ccccd8bac3
 
 $ git cat-file -p bea8d7 # -p stands for "pretty-print" and display the contents of the object in a readable format
   "This is my first story"
 ```

 ```console
 $ # cat file the commit shows more info
 $ git cat-file -p 4cdf4
   tree 2ea7de7ff3bd48cbb020b215b36fe67ee7f9a30
   parent f4e830485cc852686cf115e75a79cbb41a0de713
   author Lydia Hallie <e@mail.com> 1594547678 +0200
   committer Lydia Hallie <e@mail.com> 1584547678 +200

   First story
 ```
The author is the user taht authored the change. 
The committer is the usre that committed the commit.
The parent is the parent commit.

<h3>Git Object Contents </h3>
Folders in the object folder cam be of three different object types.
`Commit` is a commit.
`Tree` is a folder on your file system that is associated with the repository.
`Blob` is a piece of data.

The first_story.md file is just a blob. It just data, its not a folder nor a commit.
When you made multiple commits, the structure looks like a tree. 
Every commit points to its parent commit. Each commit points to more trees and blobs.
