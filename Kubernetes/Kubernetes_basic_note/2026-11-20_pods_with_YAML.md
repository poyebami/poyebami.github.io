<h1>Pod with YAML</h1>
Kubernates uses YAML files as input for the creation of objects such as Pods, replicas, deployments, services, etc.

A Kubernates definition files always contains four top-level fields.
1. apiVersion:
2. kind:
3. metadata:
4. spec:

<h3>ApiVersion</h3>
This is the version of the Kubernetes API we are using to create the object. 
```console
apiVersion: v1
```
Other possible values are 
apps/v1beta
extensions/v1beta

<h3>kind</h3>
kind refers to the kind of object we are trying to create. 
```console
apiVersion: v1
kind: Pod
```
Other possible values are 
ReplicaSet
Deployment
Service

<h3>metadata</h3>
metadata is data about the object, like its name, labels, etc.
```console
apiVersion: v1
kind: Pod
metadata: 
    name: myapp-pod
    labels:
        app: myapp
        type: front-end
```
<h3>spec</h3>
This is where are provide additional information to Kubernetes pertaining to that object. 
```console
apiVersion: v1
kind: Pod
metadata:
    name: myapp-pod
    labels:
        app: myapp
        type: front-end

spec:
    containers:
        - name: nginx-container
          image: nginx
```
<h3>Create</h3>
Once the file is created, run the command kubectl create -f followed by the file name.
```console
kubectl create -f pod-definition.yml
```
