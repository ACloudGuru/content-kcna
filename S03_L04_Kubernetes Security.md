# Kubernetes Security

## Links
- [Overview of Cloud Native Security](https://kubernetes.io/docs/concepts/security/overview/)
- [Authenticating](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)
- [Authorization Overview](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)
- [OPA Gatekeeper: Policy and Governance for Kubernetes](https://kubernetes.io/blog/2019/08/06/opa-gatekeeper-policy-and-governance-for-kubernetes/)

## Demo Reference
Log in to your Kubernetes control plane server.

Check out your kubeconfig and view the client certificate.

```
cat ~/.kube/config
```

Next, let's explore RBAC authorization.

Create a ServiceAccount.

```
kubectl create serviceaccount my-sa
```

Create a Role with permission to list Pods.

```
vi list-pods-role.yml
```

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: list-pods-role
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["list"]
```

```
kubectl apply -f list-pods-role.yml
```

Create a RoleBinding to bind the Role to the ServiceAccount.

```
vi list-pods-rb.yml
```

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: list-pods-rb
subjects:
- kind: ServiceAccount
  name: my-sa
  namespace: default
roleRef:
  kind: Role
  name: list-pods-role
  apiGroup: rbac.authorization.k8s.io
```

```
kubectl apply -f list-pods-rb.yml
```

Create a Pod that uses the ServiceAccount to retrieve a list of Pods from the API.

```
vi sa-pod.yml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: sa-pod
spec:
  serviceAccountName: my-sa
  containers:
  - name: busybox
    image: radial/busyboxplus:curl
    command: ['sh', '-c', 'while true; do curl -s --header "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)" --cacert /var/run/secrets/kubernetes.io/serviceaccount/ca.crt https://kubernetes/api/v1/namespaces/default/pods; sleep 5; done']
```

```
kubectl apply -f sa-pod.yml
```

Check the logs for `sa-pod`.

```
kubectl logs sa-pod
```
