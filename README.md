# cilium
Learn cilium

# Install Kubernetes cluster
Use [kind](https://kind.sigs.k8s.io/) to create Kubernetes cluster on local laptop  
If you have go 1.17+ and docker or podman installed:
```
> go install sigs.k8s.io/kind@v0.20.0
```
This will put kind in `$(go env GOPATH)/bin`