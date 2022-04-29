# Telemetry and Observability

## Links
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [New Relic - A Quick Introduction to Distributed Tracing](https://newrelic.com/resources/ebooks/quick-introduction-distributed-tracing)

## Demo Reference
Log in to your Kubernetes control plane server.

Create a Pod.

```
vi logging-pod.yml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: logging-pod
spec:
  containers:
  - name: busybox
    image: busybox:stable
    command: ['sh', '-c', 'while true; do echo Hello, world!; sleep 5; done']
```

```
kubectl apply -f logging-pod.yml
```

Get the logs from the Pod's container.

```
kubectl logs logging-pod -c busybox
```
