<h1>Simplifying SSH Connection with a Config File</h1>
After some troubleshooting, I tried adding a config file on Ubuntu, but it didn't work. I later realized that the config file needed to be added on the Windows `.ssh` folder instead.

<h3>Example of ssh with config file</h3>
 ```console
 $ # ssh john@dev.example.com -p 2322
 
 Host dev
        HostName dev.example.com
        User john
        Port 2322
 
 $ # Host: is the shortcut to ssh. It can be whatever you want
 $ # HostName: this is the domain name or the IP address of the server
 $ # Port: port number (default is 22)i
 $ # User: username to log in as
 $ # IdentityFile: path to your private key
 ```
 ```console
 $ # more examples
 Host targaryen
        HostName 192.168.1.10
        User daenerys
        Port 7654
        IdentityFile ~/.ssh/targaryen.key

 Host tyrell
        HostName 192.168.10.20
        
 Host *ell
        user oberyn
 
 Host * !martell
        Loglevel INFO

 Host *
        User root
        Compression yes
 ```
Loglevel control how much detail SSH prints when connecting. It's useful for debugging.
 ```console
 QUIET                  almost nothing
 FATAL                  only fatal errors
 ERROR                  only errors
 INFO                   basic info (default)
 VERBOSE                more detail
 DEBUG                  detailed debug info
 DEBUG2                 more detailed
 DEBUG3                 more detailed

 $ # DEBUG is the same as running ssh -v, DEBUG2 = -vv, DEBUG3 = -vvv
 ```
 Compression reduces the amount of data sent over the SSH connection by compressing it before sending
 ```console
 yes                    enable compression
 no                     disable compression (default)
 
 $ # yes: speeds slow or remote connection
 $ # no: not need for fast local network because it adds CPU overhead with no benefits
 $ # no: not need for transferring already compressed files because it won't help
 ```
