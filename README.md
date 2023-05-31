# Argo CD local setup

## Prerequisites

- Docker
- [kind](https://kind.sigs.k8s.io/) 
- kubectl
- [Argo CD CLI](https://argo-cd.readthedocs.io/en/stable/cli_installation/) 


## Steps

### Setup Kubernetes cluster

Use single node cluster unless requiring other deployment strategy (e.g., rolling updates)

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

### Create an application on Argo CD

Follow [step 6](https://argo-cd.readthedocs.io/en/stable/getting_started/#6-create-an-application-from-a-git-repository) or use application from another repository

NB: It's [recommended](https://argo-cd.readthedocs.io/en/stable/user-guide/best_practices/#separating-config-vs-source-code-repositories) to separate config and source code repositories.

### Deploy an application on Argo CD

Follow [step 7](https://argo-cd.readthedocs.io/en/stable/getting_started/#7-sync-deploy-the-application)

## Others

### No Docker Desktop (macOS)

Requires [Lima](https://lima-vm.io/)

```sh
limactl start --name=lima-default template://docker

docker context create lima-default \
  --docker "host=unix://$HOME/.lima/docker/sock/docker.sock"

docker context use lima-default
```
