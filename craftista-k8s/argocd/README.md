# ArgoCD Setup for Craftista

## Prerequisites
- ArgoCD installed in your cluster
- Access to ArgoCD UI or CLI

## Deploy Applications

### 1. Apply ArgoCD Applications
```bash
kubectl apply -f argocd/craftista-dev-app.yaml
kubectl apply -f argocd/craftista-staging-app.yaml
```

### 2. Verify Applications
```bash
# Check ArgoCD applications
kubectl get applications -n argocd

# Using ArgoCD CLI
argocd app list
argocd app get craftista-dev
argocd app get craftista-staging
```

### 3. Access ArgoCD UI
```bash
# Port forward to ArgoCD server
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Get admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## Features
- **Automated Sync**: Applications automatically sync when Git changes
- **Self-Healing**: ArgoCD corrects any drift from desired state
- **Namespace Creation**: Automatically creates target namespaces
- **Pruning**: Removes resources deleted from Git

## Manual Operations
```bash
# Manual sync
argocd app sync craftista-dev
argocd app sync craftista-staging

# Refresh (detect changes)
argocd app refresh craftista-dev

# View sync status
argocd app wait craftista-dev
```