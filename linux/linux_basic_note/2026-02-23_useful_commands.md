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
