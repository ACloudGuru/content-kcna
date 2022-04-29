# Kubernetes Networking

## Links
- [Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)
- [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [DNS for Services and Pods](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

## Demo Reference
Log in to your Kubernetes control plane server.

Create two Pods on two different Nodes, and have them communicate over the cluster network.

First, create a server Pod.

```
vi server-pod.yml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: server-pod
spec:
  nodeSelector:
    kubernetes.io/hostname: k8s-worker1
  containers:
  - name: nginx
    image: nginx:stable
```

```
kubectl apply -f server-pod.yml
```

Verify that the server Pod is running and obtain its cluster IP address.

```
kubectl get pod server-pod -o wide
```

Create a client Pod that makes a request to the server Pod.

```
vi client-pod.yml
```

Insert the server Pod's cluster IP address into container command.

```
apiVersion: v1
kind: Pod
metadata:
  name: client-pod
spec:
  restartPolicy: OnFailure
  nodeSelector:
    kubernetes.io/hostname: k8s-worker2
  containers:
  - name: busybox
    image: radial/busyboxplus:curl
    command: ['curl', '<Server Pod IP address>']
```

```
kubectl apply -f client-pod.yml
```

Verify that the client Pod ran successfully.

```
kubectl get pod client-pod
```

Check the log for the client Pod. You should see the Nginx welcome page HTML output.

```
kubectl logs client-pod
```
