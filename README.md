# cilium
Learn cilium

# Install Kubernetes cluster
Use [kind](https://kind.sigs.k8s.io/) to create Kubernetes cluster on local laptop  
  
If you have go 1.17+ and docker or podman installed:
```
> go install sigs.k8s.io/kind@v0.20.0
```
This will put kind in `$(go env GOPATH)/bin`  
  
Now create a new kind cluster using the configuration `kind-config.yaml`:
```
> kind create cluster --config=kind-config.yaml
```

Because you have created the cluster without a default CNI, the Kubernetes nodes are in a NotReady state:
```
> kubectl get nodes
NAME                STATUS    ROLES          AGE    VERSION
kind-control-plane  NotReady  control-plane  5m9s   v1.25.3
kind-worker         NotReady  <none>         4m45s  v1.25.3
kind-worker2        NotReady  <none>         4m46s  v1.25.3
```

# Install Cilium CLI
For more informtation about Cilium CLI installatie, see [install-the-cilium-cli](https://docs.cilium.io/en/v1.13/gettingstarted/k8s-install-default/#install-the-cilium-cli)
Execute shell script `install-cilium-cli.sh` (MACOS M2)
```
> ./install-cilium-cli.sh
```
The Cilium CLI will be installed in `/usr/local/bin`  
```
> cilium version
cilium-cli: v0.15.18 compiled with go1.21.5 on darwin/arm64
cilium image (default): v1.14.4
cilium image (stable): v1.14.5
cilium image (running): unknown. Unable to obtain cilium version, no cilium pods found in namespace "kube-system"
```
We’ll be installing the default Cilium image into the Kubernetes cluster we’ve prepared. Note also that the CLI tool is telling us that we don’t yet have a Cilium installed into the cluster. We are going to fix that right now.

# Install Cilium
Now we can use the Cilium CLI tool to install Cilium:
```
> cilium install
```
It may take a couple of minutes for the installation process to complete. In another terminal, you can use the Cilium CLI tool to watch and wait for Cilium to be fully deployed and operational:
```
> cilium status --wait
```

