# Exploring Kubernetes Architecture

## Links
- [Cluster Architecture](https://kubernetes.io/docs/concepts/architecture/)
- [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)

## Demo Reference
Log in to your Kubernetes control plane server.

Note that `kubelet` is installed as a Linux service.

```
sudo systemctl status kubelet
```

Check the default Namespaces in the cluster.

```
kubectl get namespace
```

Check the Pods in the `kube-system` Namespace. You will see various Kubernetes control plane components running as Pods in the cluster.

```
kubectl get pods -n kube-system
```
