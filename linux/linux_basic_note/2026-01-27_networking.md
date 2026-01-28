<h1>Networking</h1>

<h3>Changing host names</h3>
There are two computers and both are part of the same network (192.168.1.0). They have been assigned with IP address
192.168.1.10 and 192.168.1.11. To check the connectivity between the two server, you can run the ping command on 
one computer to the other, using the other computer's IP address.
 ```console
  $ # check the connectivity between two server
  $ ping 192.168.1.11
  Reply from 192.168.1.11: bytes=32 time=4ms TTL=117
  Reply from 192.168.1.11: bytes=32 time=4ms TTL=117
 ```
System B has database service and instead of having to remember the IP address of system B, you decided to give it a name (db).
However, if you tried to ping db, host A is unaware of a host named db.
 ```console
  $ ping db
  ping : unknown host db
 ```
To fix this issue, you need to tell system A that system B at IP address 192.168.1.11 has a name DB. To do that,  you need to add an
entry into /etc/hosts file on system A.
 ```console
  $ cat >> /etc/hosts
  192.168.1.11   db

  $ ping db
  PING db (192.168.1.11) 56(84) bytes of data
  64 bytes from db (192.168.1.11): icmp_seq=1 tt1=64 time=0.052 ms
  64 bytes from db (192.168.1.11): icmp_seq=2 tt1=64 time=0.079 ms
 ```
Whatever we put in the /etc/files is the source of truth for host A. Host A does not check to make sure if system  B's actual name is db.
For instance, running a hostname command on system B reveals that it is named host 2. But host A doesn't care. It goes by what is in the 
hosts file.
 ```console
  $ # running hostname command on system B
  $ hostname
  host-2
 ```
You can even fool system A into believing that system B is Google. Just by adding an entry into the hosts file with a IP mapping to
www.google.com. And then ping Google, and will get a response from system B.
 ```console
  $ cat >> /etc/hosts
  192.168.1.11   db
  192.168.1.11   www.google.com

  $ ping www.google.com
  PING www.google.com (192.168.1.11) 56(84) bytes of data
  64 bytes from www.goggle.com (192.168.1.11): icmp_seq=1 tt1=64 time=0.052 ms
  64 bytes from www.google.com (192.168.1.11): icmp_seq=2 tt1=64 time=0.079 ms
 ```
We have two names pointing to the same system. One is db and the other is google. We can use either name to reach system B. Translating host name
to IP address in the etc/hosts file is called `name resolution`. Ping may not always be a good command to test DNS resolution, especially if
ping is disabled on the other host. A work around will be using nslookup and dig.

<h3>DNS</h3>
There are other systems in the environment each with their own IP address and names. In each system, we need to specify which are the other 
systems in the environment. However, with more and more systems added in the environment, it can be a lot to manage. If one system's IP changed,
you will need to modify the entries on the other systems. To make managing the hosts and their IP address easier, we need to move everything into a 
single server. This is called a DNS server. We point all host to look up that server if they need to resolve a hostname to an IP address instead
of its own /etc/hosts file. 

For instance, our DNS server has the IP 192.168.1.100. Every host has a DNS resolution configuration file at /etc/resolv.conf. You add an entry into it
specifying the address of the DNS server.
 ```console
 $ cat /etc/reslov.conf
 nameserver     192.168.1.100

 $ ping db
 PING db (192.168.1.11) 56(84) bytes of data
 64 bytes from db (192.168.1.11): icmp_seq=1 tt1=64 time=0.052 ms
 64 bytes from db (192.168.1.11): icmp_seq=2 tt1=64 time=0.079 ms
 ```
Once this is configured on all of your hosts, every time a host comes across a hostname that it does not know about, it looks it up from the DNS server. If the IP of
any of the hosts was to change, we can update the DNS server. You don't have to put any entries on the host file, but it doesn't mean we can't have entries in the hosts
file. 

For instance, you created a test server for your own needs and don't think others would need to resolve this server by its name. So the test server IP doesn't have to be added 
to the DNS server. You can add any entry to the host file to ping the server. However, no other server will be able to do that. 

A system is able to use hostname to IP mapping from its hosts file locally as well as from a remote DNS server. What if there is an entry in both places? One in the host file and 
another in DNS? For instance, I have an entry in my local files set to 192.168.1.115 called test and someone added an entry for the same host called test to 192.168.1.116 on the 
DNS server. The host files looks at the local /etc/hosts file and the looks at the name server. If it finds the entry in the local hosts file, it uses that. If not, it looks for that in
the DNS server. But that order can be changed. The order is defined by an entry in the file /etc/nsswitch.conf, the line with the host entry.  

 ```console
 cat /etc/nsswitch.conf
 ...
 hosts:     files   dns
 ...
 ```
The order is first files and then followed by the DNS. Files refers to /etc/hosts file and DNS refers to the DNS server. So for every host anme, the host first looks into the local host file, and if 
it cannot find it there, it then looks at the DNS server. This order can be modified by editing the entry in the file. As of this order, whenever I ping test, it will be the entry for 192.168.1.115. 

<h3>Pinging a server that is not local file and DNS server</h3>

