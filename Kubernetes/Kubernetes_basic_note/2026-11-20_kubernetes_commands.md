<h1>Kubernetes Commands</h1>

<h3>Pods commands</h3>
```console
$ # create pods
kubectl create -f <name_of_pod>.yaml

$ # list pods
kubectl get pods

$ # list additional information on pods
$ # shows IP, NODES, etc
kubectl get pods -o wide

$# get information about the pod
kubectl describe pods myapp-pod

$# delete pod
kubectl delete pod myapp-pod

$# create or updates cluster resources from YAML or JSON files
kubectl apply -f redis-pod.yaml
```

<h1>Additional Complex Command</h1>
```console
kubectl run redis --dry-run -o yaml
```
This command is used for quick creation of a single pod. Used for fast debugging, testing, and troubleshooting. 
`--dry-run` simulates the command without sending anything to the cluster. Meaning nothing gets created.
`-o yaml` prints the results as YAML

```console
kubectl run redis --image=redis --dry-run=client -o yaml
```
Using bare `--dry-run` was deprecated and later removed.
`--dry-run=client` builds the object locally and prints it. (no API call for validation)
`--dry-run=server` sends the request to the API server for full vlidation, but doesn't persist it.

```console
$ # generates the pods as a YAML and sends the output into a file
kubectl run redis --image=redis --dry-run=client -o yaml > redis-pod.yaml
$ # after cat the file to check the information and then use kubectl to create the file. 
```
