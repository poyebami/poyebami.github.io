<h1>Useful Linux Commands</h1>

<h3>Updating Linux System Local Package datebase</h3>
Always run apt update before installing new packages. Package manager keep a local database of those packages. Think of it like the index in a book or the menu at a restaurant.

Updates the database so that your computer knows about all the recent changes to the repo, like new packages or new versions of older packages
```console
 $ sudo apt update
```

Compares your local datebase with the list of pacakges you actually have installed and upgrades the installed packages that are older than the ones on the repo.
```console
 $ sudo apt upgrade
```

Using sudo apt update alone does not update your system, just your datebase. Using sudo apt upgrade alone can upgrade your system, but if you're using an older version of the database, you may not get the latest versions of your packages. Usually use both of these commands together,
`sudo apt update && sudo apt upgrade`. This gives us the latest database and then upgrades our software to the latest version on that database, guaranteeing that you are completely up-to-date.

<h3>Switching to the Root User</h3>
 ```console
 $ sudo i

 $ # exit to return to normal user
 $ # type EXIT or press Ctrl+D 
 ```

<h3>df command </h3>
 ```console
 $ # displays the amount of available and used disk space on mounted file systems
 $ df
 ```

<h3>Find Command </h3>
 ```console 
 $ # find and list the absolute path of file
 $ find . -name basketball.txt

 $ # find and list all .txt files 
 $ find . -name "*.txt"

 $ # find and list all that starts with prosper*
 $ find ~ -name "prosper*"
 /home/vagrant/prosper_v2
 /home/vagrant/prosper
 /home/vagrant/prosper_1

 $ # find and list all txt files in a directory
 $ find animals/ -name "*txt" 
 animals/mammals/birds/parrot.txt
 animals/mammals/birds/penguins.txt
 animals/aquatic/fish/shark.txt

 $ # find and list files only
 $ find . -type f
 $ # find and list files only in home directory
 $ find ~ -type f

 $ # find and list all directory
 $ find . -type d 
 ```
<h3>Reading Files Without Opening Them</h3>
 ```console
 $ # print entire files
 $ cat /etc/hosts

 $ # scroll throufh large files 
 $ less /var/log/syslog

 $ # first N lines of a file
 $ head -20 server.log

 $ # last N lines of a file
 $ tail -f /var/log/nginx/access.log
 ``` 
<h3>grep</h3>
The `grep` command search for text inside files.
 ```console
 $ # find a word in one file
 $ grep "prosper" soccer.txt
 
 $ # search in all .txt files
 $ grep "prosper" *.txt
 ```
 ```console
 $ # case-insensitive
 $ grep -i "goal" soccer.txt
 
 $ # show line number
 $ grep -n "prosper" readme.txt
 1: hi this is prosper
 4: hi prosper. this is the readme.txt file

 $ # count matching lines
 $ grep -c "prosper" readme.txt

 $ # show line that Don't match
 $ grep -v "prosper" readme.txt

 $ # search recursively in directories
 $ grep -r "prosper" ./
 ./readme.txt: hi this is prosper
 ./readme.txt: hi prosper. this is the readme.txt file
 ```
Combining Flags
 ```console
 $ # case-insensitive + line numbers
 $ grep -in "goal" soccer.txt

 $ # recursive + line numbers
 $ grep -rn "goal" ../premier_league/

 $ # case-insensitive + filename only
 $ grep -il "goal" *.txt
 ```
