<h1>How top Copy Files from Local to SSH</h1>
To copy a file from your local machine to a remote server over SSH is to use `scp`.

<h3>Single Files</h3>
 ```console
 scp /path/to/local/file.txt username@remote_host:/path/to/remote/directory/

 scp /mnt/c/Users/Downloads/document.pdf ubuntu@192.168.1.50:.
 ```
<h3>Copy a Full directory</h3>
 ```console
 scp -r /path/to/local/folder username@remote_host:/path/to/remote/directory/

 scp -r /mnt/c/Users/mideo/Downloads/link-shortener ubuntu@192.168.1.50:.
 ```
