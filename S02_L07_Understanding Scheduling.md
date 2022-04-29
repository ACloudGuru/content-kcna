# Understanding Scheduling

## Links
- [Kubernetes Scheduler](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

## Demo Reference
Log in to your Kubernetes control plane server.

Create a YAML manifest for a Pod with a nodeSelector.

```
vi fast-pod.yml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: fast-pod
spec:
  containers:
  - name: nginx
    image: nginx:stable
  nodeSelector:
    nodeclass: fast
```

Create the Pod.

```
kubectl apply -f fast-pod.yml
```

Check the Pod status. Note that it is `Pending`. This means it is not able to start up yet, since it has not been assigned to a Node.

```
kubectl get pods
```

Add the `nodeclass` label to a Node.

```
kubectl label nodes k8s-worker1 nodeclass=fast
```

Check the Pod status again.

```
kubectl get pods -o wide
```
