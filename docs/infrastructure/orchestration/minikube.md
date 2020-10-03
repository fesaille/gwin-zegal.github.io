# Minikube <badge-stars repo='kubernetes/minikube'></badge-stars> <badge-doc href="https://minikube.sigs.k8s.io"></badge-doc>

## Installation: local cluster with minikkube

Direct download via:

```terminal
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
```

Driver:

The vmware driver supports virtualization across all VMware based hypervisors.

https://minikube.sigs.k8s.io/docs/drivers/vmware/

r=https://api.github.com/repos/machine-drivers/docker-machine-driver-vmware
curl -LO $(curl -s $r/releases/latest | grep -o 'http.*darwin_amd64' | head -n1) \
 && install docker-machine-driver-vmware_darwin_amd64 \
   /usr/local/bin/docker-machine-driver-vmware


[^1]: [Install minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
