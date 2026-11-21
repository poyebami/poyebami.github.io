<h1>etcd for Beginners</h1>
etcd is a distributed reliable key-value store that is simple, secure, and fast. 

<h3>Key Value Store</h3>
It stores a value against a key.

 ```console
 Key: name
 Value: John Doe

 Key: age
 Value: 45

 Key: user:john_doe
 Value: name=John Doe, age=45, location=New York, salary=5000
 ```
<h3>How to install etcd</h3>
Download the binary from the GitHub Release page. Extrat it and run the etcd executable. 

When you run etcd, it starts a service that listens on port 2379 by default. You can run it as a system service or as a pod on a Kubernetes cluster. You can attact any clients to the etcd services to store and retrieve information. A default client that comes with etcd is the `etcd control client` or `etcdctl`. 

