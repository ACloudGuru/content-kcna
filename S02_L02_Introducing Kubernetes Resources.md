# Introducing Kubernetes Resources

## Links
- [Kubernetes API Terminology](https://kubernetes.io/docs/reference/using-api/api-concepts/#standard-api-terminology)
- [Understanding Kubernetes Objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)
- [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)
- [Init Containers](https://kubernetes.io/docs/concepts/workloads/pods/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Demo Reference
Log in to your Kubernetes control plane server.

Get a list of resources available in the cluster.

```
kubectl api-resources
```

Get detailed documentation for the `pods` resource.

```
kubectl explain pod
```

Create a YAML manifest file for a Pod.

```
vi my-pod.yml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: nginx
    image: nginx:stable
```

Create the Pod.

```
kubectl apply -f my-pod.yml
```

Get a list of Pods in the `default` Namespace.

```
kubectl get pods
```

Delete the Pod.

```
kubectl delete pod my-pod
```
