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
 ```console
 $ # change DNS server to Google's DNS 
 $ vi /etc/resolv.conf
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
 $ # find the ip address of the DNS Server
 $ cat /etc/resolv.conf
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
 $ # change the order of resolution 
 $ vi /etc/nsswitch.conf
 ```
 ```console
 cat /etc/nsswitch.conf
 ...
 hosts:     files   dns
 ...
 ```
The order is first files and then followed by the DNS. Files refers to /etc/hosts file and DNS refers to the DNS server. So for every host anme, the host first looks into the local host file, and if 
it cannot find it there, it then looks at the DNS server. This order can be modified by editing the entry in the file. As of this order, whenever I ping test, it will be the entry for 192.168.1.115. 

<h3>Pinging a server that is not local file and DNS server</h3>
For instance, I tried to ping www.facebook.com. www.facebook.com is not in the /etc/hosts file and its not in the DNS server. And in that case, the ping will fail. 
 ```console
 $ ping www.facebook.com
 ping: www.facebook.com: Temporary failure in name resloution
 ```
You can add another entry in the host resolv.conf file to point to a name server that knows facebook.com 8.8.8.8 is a public name server available on the internet hosted by google that knows 
about all websites on the internet. You can have multiple name servers like this configured on your host, but then you will have to configure that on all hosts in your network. You already
have a name server within your network configured on all host, so in that case, you can configure the DNS server itself to forward any unknown host names to the public name server on the internet.
Doing so you should be able to ping external sites such as facebook.com.
 ```console
 cat >> /etc/resolv.conf
 nameserver     192.168.1.100
 nameserver     8.8.8.8

 $ ping www.facebook.com
 PING star-mini.c1or.facebook.com (157.240.13.35) 56(84) bytes of data.
 64 bytes from edge-star-mini-shv-02-sin6.facebook.com (157.240.13.35): icmp_seq=1 tt1=50 time=5.70 ms
 ```

<h3>Domain Names</h3>
The last portion of the domain name, the .com, .net, .edu, .org, etc are the top-level domains. They represent the intent of the website. .com is for commercial or general purpose, 
.net for network or general purpose, .edu is for educational organizations, .org is for non-profit organization, etc. For instance: www.google.com
 ```console
 .          - is the root
 .com       - is the top level domain name
 google     - is the doman name assigned to google
 www        - is a subdomain

 the subdomains helps in further grouping things together under google
 maps.google.com            google's map service
 drive.google.com           google's storage service
 apps.google.com            google's mobile apps
 mail.google.com            gooogle's email service

 you can further divide each of these into as many subdomains based on your needs.
 ```
If you try to search any of these domain names (apps.google.com) frim within your organization, your request first hits your organizational's internal DNS server. 
It doesn't know who apps or google is, so it forwards your request to the internet. On the internet, the IP address of the server serving apps.google.com may be resolved
with the help of multiple DNS server. A root DNS server looks are your request and points you to a DNS server serving .com. A .com DNS server looks at your request and
forward you to google, and google's DNS server provides you the IP of the server serving applications. In order to speed you all future resolves, your organization's 
DNS server may choose to cache this IP for a period of time, typically a few seconds up to a few minutes. That way, it doesn;t have to go through the whole
process again. 

How the process is the name for www.google.com, it is the same under your organization's DNS server. It also have web, mail, drive, www, pay, hr, are its subdomain. We put the entries
under /etc/resolv.conf and have now introduced more standard domains like web.mycomany.com or db.mycompany.com. Now, when you ping web, you can no longer get a response. It is because there 
is no record by the name web on my DNS server. Instead, it is web.mycomapny.com and must use it to ping it. However, if you want to use web instead of web.mycomapny.com, you make an entry
into your host's /etc/resolve.conf file called search and s epcify the domain name you want to append.
 ```console
 $ cat >> /etc/resolv.conf
 nameserver         192.168.1.100
 search             mycompany.com


 192.168.1.10       web.mycompany.com
 192.168.1.11       db.mycompany.com
 192.168.1.12       nfs.mycompany.com
 192.168.1.13       web-1.mycompany.com
 192.168.1.14       sq1.mycompany.com
 ```

<h3>Record Tpyes </h3>
How are records stored in the DNS server? It stores IP to host names. That's known as A record. Storing IPv6 to host names is known as quad A records. Mapping one name to another name is 
called CNAME records.
 ```console
 A          web-server          192.168.1.1
 AAAA       web-server          2001:0db8:85a3:0000:0000:8a2e:0370:7334
 CNAME      food.web-server     eat.web-server,hungry.web-server
 ```
For CNAME record,  you may have multiple aliases for the same applications like a food delivery service that can be reached at eat or hungry. 

<h3>Tools to test DNS resolution</h3>
Mapping may no always be the right tools to test DNS resolution. There are a few other tools such as nslookup. You can use nslookup to query ahost name from a DNS server.
 ```console
 $ nslookup www.google.com
 Server:        8.8.8.8
 Address:       8.8.8.8#53

 Non-authoritative answer:
 Name:      www.google.com
 Address:   172.217.0.132
 ```
Remember that nslookup does not consider the entries in the local /etc/hosts file. The same goes for Dig. It returns more details in a similar form as is stored on the server.
 ```console
 $ dig www.google.com
 ... more detail information
 ```

<h1>Networking Basics</h1>

<h3>Switching</h3>
Let say there are two system (A and B). How does system A reach B? We connect them to a `switch`, and a switch creates a network containing the two systems. To connet them to a
switch, we need an interface on each host, physical or virtual depending on the host. To see the interfaces for the host, we use the IP link command.
 ```console
 $ # to see the interface for the host, in this case eth0
 $ ip link 
 eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_code1 state UP mode
 DEFAULT group default qlen 1000
 ```
Let's assume it's a network with the address 192.168.1.0. We then assign the systems with IP addresses on the same network. For this, we use the command
 ```console
 $ # adding the systems with their own IP address to the same network, in this case eth0
 
 $ # systemA
 $ ip addr add 192.168.1.10/24 dev eth0
 
 $ # systemB
 $ ip addr add 192.168.1.11
 ```

<h3>Routing </h3>
There is another network containing systemC and systemD at the address 192.168.2.0. How does a system in one network reach a system in the other? 
How does systemB with the IP 1.11 reach systemC with the IP 2.10 on the other network?  That is where a router comes in. A router helps connect two network
together. Think of it as another server with many network ports. Since it connects to the two separate networks, it gets two IPs assigned, one on each network.

When systemB tires to send a packet to system  C, how does it know where the router is on the network to send the packet through? The router is just another device
on the network. That's where we configure the systems with a gateway or a route. If the network was a room, the gateway is the door to the outside world, to other
networks, or the internet. The systems need to know where the door is to go through that. To see the existing routing configuration on a system, run the route command.
 ```console
 $ # displays the kernel's routing table
 $ route
 Kernel IP routing table
 Destination    Gateway     Genmask     Flags Metric Ref    Use Iface
 $ # here we see that there is connections
 ```
 ```console
 $ # configure a gateway on a system from a different network
 $ ip route add 192.168.2.0/24 via 192.168.1.1
 
 $ # after connecting the two networks
 $ route                                                                                                                                                                                                                                                                                                                
 Kernel IP routing table                                                                                                                                                                                                                                                                                                
 Destination    Gateway          Genmask            Flags Metric Ref    Use Iface   
 192.168.2.0    192.168.1.1      255.255.255.0      UG    0      0        0 eth0  
 ```
 We have to configure it on all systems.

These systems need access to the internet. Say they need access to Google at 172.217.194.0 network on the inernet, so you connect the routher to the internet, and then add 
a new route in your routing tavle to route all traffic to the network 172.217.194.0 through your router.
 ```console
 $ # add a route to 172.217.194.0/24 via the gateway at 192.168.2.1
 $ ip route add 172.217.194.0/24 via 192.168.2.1

 $ # adds default via 192.168.2.1
 $ ip route add default via 192.168.2.1

 $ # add a default route (for all address)  via the local gateway 192.168.1.1 that can be reached on device em1
 $ ip route add default via 192.168.1.1 dev em1

 $ # add a route to 192.168.1.0/24 that can be reached on device em1
 $ ip route add 192.168.1.0/24 dev em1
 ```
Instead of the word default, you could also say 0.0.0.0. It means any IP destination. 

Let say there is another router in your network, one the internet and another for internal private networks. You will need to have two seperate entries for each network, one entry for the internal
private network and another default gateway for all other networks. 

<h3>Networking Commands </h3>
 ```console
 $ # display ip commands and arguments
 $ ip help
 
 $ # diplay address commands and arguments 
 $ # ip addr help

 $ # display link commands and arguments
 $ ip link help

 $ # display neighbour commands and arguments
 $ ip neigh help

 $ # list and modify interfaces on the host
 $ ip link 

 $ # see the IP address assigned to these interface
 $ ip addr

 $ # use to set IP addresses on the interface
 $ ip addr add 192.168.1.10/24 dev eth0

 $ # changes made using these commands are only valid till a system restart. 
 $ # if you want to persist these changes, you must set them in the /etc/network/interfaces file.

 $ # view the routhing table
 $ route
 $ ip route

 $ # add entries into the routing table
 $ ip route add 192.168.1.0/24 via 192.168.

 $ # alter the status of the interface
 $ # bring em1 online
 $ ip link set em1 up

 $ # bring em1 offline
 $ ip link set em1 down

 $ # set the MTU on em1 to 9000
 $ # MTU (maximum transmission unit) defines the largest packet size (in bytes) allowed over an interface , with the standard Ethernet default being 1500
 $ # configuring an MTU of 9000 units (Jumbo Frames) can increase throughout for large data transfers but requires support from all networking equipment (switches, routers) in the path
 $ ip link set em1 mtu 9000

 $ # enable promiscuous mode of em1
 $ # promiscuous mode in linux allows a network interface card (NIC) to pass all receieved traffic to the operating system, regardless of the destination MAC address.
 $ # crucial for network sniffing, bridging (VMware/KVM), and monintoring.
 $ ip link set em1 promisc on
 ``` 

<h1>Troubleshooting Network</h1>

<h3>Checking Host's IP connectivity</h3>
Check the local interface by running the IP link command and ensure the primary interface is up. 
 ```console
 $ ip link
 1. lo <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc
   ...

 2. enp1s0f1: <BROADCAST, BROADCAST, MULTICAST, UP> mtu 1  500 qdisc
     fq_code1 state UP mode DEFAULT group default qlen 1000
     link/ether 08:97:98:6e:55:4d brd ff:ff:ff:ff:ff:ff
 ```
 We can see that enq1s0f1 is up

<h3>Checking DNS Resolution</h3>
Run an nslookup command aganist the hostname and make sure it is resolving to a valid IP. Make sure everything is correct
 ```console
 $ nslookup caleston-repo-01
 Server:        192.168.1.100
 Address:       192.168.1.100 #53

 Non-authoritative answer:
 Name:  caleston-repo-01
 Address: 192.168.2.5
 ```
<h3>Check Connectivity</h3>
Try to ping the remote server to check if we get a response. 
 ```console
 $ ping caleston-repo-01
 PING caleston-repo-01 (192.168.2.5) 56(84) bytes of data.
 ^C
 --- localhost ping statistics ---
 3 packets transmitted, 0 received, 100% packet lost, time 2034ms
 ```
 There is no response. We send three packets and receieved zero back. There is a 100% packet loss. Ping is not the best way to check
 for connectiviity becuase many networks would have disabled it. 

<h3>Checking the route</h3>
To troubleshoot an issue with the route, we run the traceroute command. 
 ```console
 $ # show the number of hops, or devices, between the source, the system and the repo server
 $ # show problem with any of the devices in the network route between the source and destination
 $ traceroute 192.168.2.5
 Tracing route to example.com [192.168.2.5]
 over a maximum of 30 hops: 
 1  <1 ms   <1 ms   <1 ms   192.168.1.1
 2  <2 ms   <1 ms   <1 ms   192.168.2.1
 3   *       *       *      Request timed out.
 ```
 From the output, we see that there is two routers, the first one at 192.168.1.1 and the second at 192.168.2.1. The connection to both 
 of them is okay. However, the request timed out between the second router and the server.
 
<h3>Checking Service</h3>
Check if the HTTP process is running on port 80. We use the netstat command.
 ```console
 $ # print the information of network connections, routing tables, and several other network statistics
 $ netstat -an  | grep 80   | grep -i Listen
 tcp6   0   0 :::80     :::*        Listen
 ```

<h3>Checking Interfaces</h3>
Checking the interface using IP link command.
 ```console
 $ ip link
 1: lo <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc
    ...

 2. enp1s0f1: <BROADCAST, BROADCAST, MULTICAST, UP> mtu 1500 qdisc
     fq_code1 state DOWN mode DEFAULT group default qlen 1000
     link/ether 08:97:98:34:52:12 brd ff:ff:ff:ff:ff:ff
 ```
In this case, the interface is down. We enable UP using IP link set dev up command
 ```console
 $ ip link set dev enp1s0f1 up
 ```
