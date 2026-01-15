<h1>Generating and Using SSH Keys in Bash </h1>

```console
$ # go to the root folder
$ cd ~

$ # hidden folder for making ssh keys
$ cd .ssh

$ # making ssh key
$ ssh-keygen # enter name and passphrase

$ # don't share private key
$ ls
$ test  test.pub # .pub is public key

$ # show the key
$ cat test.pub # copy the key
 ```
After copying the public key, go to GitHub. Go to setting and selected SSH and GPG keys. Click new ssh key. Paste the ssh key and enter a label for which computer it is.
When cloning from GitHub, make sure to select code and select SSH. 
