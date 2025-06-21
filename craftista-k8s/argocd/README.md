# ArgoCD GitOps for Craftista

Complete GitOps setup for Craftista microservices deployment using ArgoCD.

## Quick Setup

### 1. Install ArgoCD
```bash
# Create namespace and install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Wait for installation
kubectl wait --for=condition=available --timeout=300s deployment/argocd-server -n argocd
```

### 2. Expose ArgoCD (GKE LoadBalancer)
```bash
# Change to LoadBalancer service
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

# Get external IP
kubectl get svc argocd-server -n argocd
```

### 3. Get Admin Credentials
```bash
# Get admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

# Login details:
# Username: admin
# Password: (output from above command)
```

### 4. Deploy Applications

#### Kustomize-based Applications
```bash
# Deploy Craftista applications (Kustomize)
kubectl apply -f craftista-dev-app.yaml
kubectl apply -f craftista-staging-app.yaml
```

#### Helm-based Applications
```bash
# Deploy Craftista applications (Helm)
kubectl apply -f craftista-dev-helm-app.yaml
kubectl apply -f craftista-staging-helm-app.yaml
```

#### Verify Deployment
```bash
# Check all applications
kubectl get applications -n argocd
```

## Access Applications

### ArgoCD UI
- **URL**: `https://<ARGOCD-EXTERNAL-IP>`
- **Username**: `admin`
- **Password**: (from step 3)

### Get Application LoadBalancer IPs

#### Via kubectl
```bash
# Development environment
kubectl get svc -n dev

# Staging environment  
kubectl get svc -n staging

# Specific service IP
kubectl get svc craftista-frontend-service -n dev -o jsonpath='{.status.loadBalancer.ingress[0].ip}'
```

#### Via ArgoCD UI
1. Click on application (`craftista-dev`, `craftista-staging`, `craftista-dev-helm`, or `craftista-staging-helm`)
2. Click on Service resources (e.g., `craftista-frontend-service`)
3. Check **Status** tab for External IP
4. Or use **Network** tab for all service IPs

## Application URLs
Once deployed, access your services:
- **Frontend**: `http://<FRONTEND-IP>:3000`
- **Catalogue**: `http://<CATALOGUE-IP>:5000`
- **Recommendation**: `http://<RECOMMENDATION-IP>:8000`
- **Voting**: `http://<VOTING-IP>:8060`

## GitOps Workflow

### Automated Deployment
1. **Jenkins** builds images and updates manifests
2. **ArgoCD** detects Git changes automatically
3. **Applications** deployed to dev/staging environments
4. **Self-healing** corrects any configuration drift

### Manual Operations
```bash
# Sync applications manually (Kustomize)
argocd app sync craftista-dev
argocd app sync craftista-staging

# Sync applications manually (Helm)
argocd app sync craftista-dev-helm
argocd app sync craftista-staging-helm

# Refresh to detect changes
argocd app refresh craftista-dev

# View application details
argocd app get craftista-dev
```

## Features

### Automated Sync
- Monitors Git repository for changes
- Automatically deploys updates
- Configurable sync policies

### Self-Healing
- Detects configuration drift
- Automatically corrects differences
- Maintains desired state

### Multi-Environment
- **Development**: `dev` namespace
- **Staging**: `staging` namespace
- Isolated deployments with RBAC

### Rollback Support
- Easy rollback to previous versions
- Git-based version history
- Point-in-time recovery

## Monitoring

### Application Status
```bash
# Check application health
kubectl get applications -n argocd

# Detailed application info
argocd app get craftista-dev --show-params
```

### Sync Status
- **Synced**: Application matches Git state
- **OutOfSync**: Differences detected
- **Unknown**: Unable to determine state

### Health Status
- **Healthy**: All resources running properly
- **Progressing**: Deployment in progress
- **Degraded**: Some resources have issues
- **Missing**: Resources not found

## Troubleshooting

### Application Not Syncing
```bash
# Check application events
kubectl describe application craftista-dev -n argocd

# Force refresh
argocd app refresh craftista-dev

# Manual sync
argocd app sync craftista-dev
```

### Repository Access Issues
```bash
# Check repository connection
argocd repo list

# Test repository access
argocd repo get https://github.com/HEMAAAAA/craftista_automation.git
```

### Resource Issues
```bash
# Check resource status in ArgoCD UI
# Or use kubectl to check specific resources
kubectl get pods -n dev
kubectl describe pod <pod-name> -n dev
```

## Security

### RBAC
- Environment-specific service accounts
- Namespace isolation
- Role-based permissions

### Git Repository
- Private repository support
- SSH key authentication
- Token-based access

### Network Security
- LoadBalancer with external IPs
- Service-to-service communication
- Network policies (optional)

## Best Practices

1. **Use Git branches** for different environments
2. **Monitor sync status** regularly
3. **Set up notifications** for sync failures
4. **Use health checks** for applications
5. **Implement proper RBAC** for team access
6. **Regular backup** of ArgoCD configuration

## Support

### Common Commands
```bash
# List all applications
argocd app list

# Get application details
argocd app get <app-name>

# Sync application
argocd app sync <app-name>

# Delete application
argocd app delete <app-name>
```

### Useful Links
- ArgoCD Documentation: https://argo-cd.readthedocs.io/
- Kustomize Documentation: https://kustomize.io/
- Kubernetes Documentation: https://kubernetes.io/docs/