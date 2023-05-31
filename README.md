# Argo CD local setup

## Prerequisites

- Docker
- [kind](https://kind.sigs.k8s.io/) 
- kubectl
- [Argo CD CLI](https://argo-cd.readthedocs.io/en/stable/cli_installation/) 


## Steps


### Setup Kubernetes cluster

```sh
kind create cluster --config cluster.yaml
```

### Install Argo CD

Steps below are based on [ArgoCD's Getting Started](https://argo-cd.readthedocs.io/en/stable/getting_started/) 

```sh
kubectl create namespace argocd

# use the manifest with UI included
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# for accessing the admin UI
kubectl port-forward -n argocd svc/argocd-server 8080:443

# for https://localhost:8080/
argocd admin initial-password -n argocd
```
