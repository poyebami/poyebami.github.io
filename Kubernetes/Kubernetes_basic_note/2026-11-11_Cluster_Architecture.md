<h1>Cluster Architecture</h1>
A Kubernetes cluster consists of a control plane plus a set of worker machine, called nodes, that run containerized applications. Each cluster needs at least one worker node in order to run Pods.

Kubernetes cluster consists of a set of nodes, that host applications in the form of containers. 

<h3>Master Node / Control Plane Components</h3>
The control plane manages the worker nodes and the Pods in the cluster. The master node uses a set of components together known as the `control plane components`.

The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events. It also acts as the brain of the cluster, maintaining the desired state, and the managing the lifecycle of containerized application across worker nodes. 

ETCD:
Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data. 
