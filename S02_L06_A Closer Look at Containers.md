# A Closer Look at Containers

## Links
- [Containers](https://kubernetes.io/docs/concepts/containers/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)

## Demo Reference
Log in to your Kubernetes control plane server.

Check the YAML manifest file for a Pod that was created in an earlier lesson:

```
cat my-pod.yml
```

Focus on the `containers` section. Each element in this list defines a container that will run within the Pod.
