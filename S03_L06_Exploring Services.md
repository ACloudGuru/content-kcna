# Exploring Services

## Links
- [Service](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

## Demo Reference
Log in to your Kubernetes control plane server.

Create a Deployment with multiple replicas.

```
vi web-deployment.yml
```

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-deployment
  template:
    metadata:
      labels:
        app: web-deployment
    spec:
      containers:
      - name: nginx
        image: nginx:stable
```

```
kubectl apply -f web-deployment.yml
```

Check the Deployment's Pods.

```
kubectl get pods -o wide
```

Create a Service that points to the Deployment's Pods using the `app` label.

```
vi web-service.yml
```

```
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  type: ClusterIP
  selector:
    app: web-deployment
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

```
kubectl apply -f web-service.yml
```

Check the Service status and get its cluster IP address.

```
kubectl get service web-service
```

Use the cluster IP to test the service. **Note**: The cluster IP works from the Kubernetes control plane node due to the routing rules managed by kube-proxy.

```
curl <Service cluster IP address>
```
