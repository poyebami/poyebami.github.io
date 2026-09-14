<h1>Adding SSH to a machine</h1>
1. To add SSH to a machine, you need to install openssh-server.
 ```console
 $ sudo apt install openssh-server
 ```
2. After install openssh-server, you need to enable it.
 ```console
 $ # enable it to start on boot, and start it 
 $ sudo systemctl enable ssh
 $ sudo systemctl start ssh
 ```
3. You need to check if ssh is running
 ```console
 $ sudo systemctl status ssh
 ```
