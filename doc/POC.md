# Proof of Concept for deploying system with ArgoCD

## Installing and configuring command access to the ArgoCD GUI in a cluster

### Preconditions

- minikube installed on a local machine
- minikube cluster created

### Preparation

1. Install Argo CD
```
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

3. Expose ArgoCD service in a background:
```
   kubectl port-forward svc/argocd-server -n argocd 8080:443 &
```

## Command Access 

1. Install the latest version of ArgoCD CLI
```
    curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
    sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
    rm argocd-linux-amd64
```
 
2. Sign in to ArgoCD by using initial admin-secret
```
    argocd admin initial-password -n argocd
```
 
3. Login to ArgoCD via CLI and change password
```
    argocd login localhost:8080
    argocd account update-password
```

4. Save password in a safe place and provide credentials to the team

## Result

Now you can access ArgoCD interface via [browser](https://localhost:8080)