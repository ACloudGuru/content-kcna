# Exploring Kubernetes Storage

## Links
- [Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)
- [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Secrets](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Rook](https://rook.io/)

## Demo Reference
Log in to your Kubernetes control plane server.

Create a Pod that writes some data to an external volume.

```
vi volume-pod.yml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: volume-pod
spec:
  restartPolicy: OnFailure
  containers:
  - name: busybox
    image: busybox:stable
    command: ['sh', '-c', 'echo Hello, world! > /voldata/hello.txt; sleep 3600']
    volumeMounts:
    - name: voldata
      mountPath: /voldata
  volumes:
  - name: voldata
    emptyDir: {}
```

```
kubectl apply -f volume-pod.yml
```

Run a command inside the container to read the output from the volume.

```
kubectl exec volume-pod -- cat /voldata/hello.txt
```
