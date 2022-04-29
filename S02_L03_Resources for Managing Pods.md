# Resources for Managing Pods

## Links
- [Workload Resources](https://kubernetes.io/docs/concepts/workloads/controllers/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Demo Reference
Log in to your Kubernetes control plane server.

Create a YAML manifest for a Deployment.

```
vi my-deployment.yml
```

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:stable
```

Create the Deployment.

```
kubectl apply -f my-deployment.yml
```

Check the Deployment status.

```
kubectl get deployment
```

View the ReplicaSet and Pods that were automatically created.

```
kubectl get replicaset

kubectl get pods
```

Use one of the Pod names to try and delete a Pod.

```
kubectl delete pod <Pod name>
```

Check the list of Pods again. You should see that the deleted Pod was replaced with a new Pod almost immediately.

```
kubectl get pods
````

Create a Deployment with an imperative command.

```
kubectl create deploy imp-deploy --image=nginx:stable --replicas=2
```
