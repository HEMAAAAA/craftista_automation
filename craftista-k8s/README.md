# Craftista Kubernetes Setup

## Prerequisites
- Kubernetes cluster (minikube, EKS, GKE, or AKS)
- kubectl configured to access your cluster
- Sufficient cluster resources (2GB RAM, 2 CPU cores minimum)
- Kustomize (built into kubectl v1.14+)

## Deployment Solutions

### 1: Using Kustomize (Recommended)
```bash
# Deploy to development environment
kubectl apply -k overlays/dev/

# Deploy to staging environment
kubectl apply -k overlays/staging/

# View what will be deployed (dry-run)
kubectl kustomize overlays/dev/
kubectl kustomize overlays/staging/
```
### 2. Verify Deployment
```bash
# Check pods in dev namespace
kubectl get pods -n dev

# Check services in dev namespace
kubectl get svc -n dev

# Check pods in staging namespace
kubectl get pods -n staging

# Check services in staging namespace
kubectl get svc -n staging
```

### 3. Access the Application
```bash
# Get LoadBalancer IPs (if using cloud provider)
kubectl get svc craftista-frontend-service -n dev
kubectl get svc craftista-frontend-service -n staging

# For local clusters (minikube), use port-forward
kubectl port-forward svc/craftista-frontend-service 3000:3000 -n dev
```

## Architecture Overview
- **Frontend**: Node.js application (Port 3000)
- **Catalogue**: Python Flask application (Port 5000) with MongoDB
- **Recommendation**: Go application (Port 8000)
- **Voting**: Java Spring Boot application (Port 8060) with PostgreSQL

## RBAC Configuration
- **dev-role**: Permissions for development team
- **stage-role**: Permissions for QA team
- Both roles have access to pods, services, and deployments in their respective namespaces

## Storage Requirements
- MongoDB: 1Gi persistent storage
- PostgreSQL: 1Gi persistent storage
- StorageClass: `standard` (modify if different in your cluster)

## Troubleshooting
```bash
# Check pod logs
kubectl logs <pod-name> -n <namespace>

# Describe pod for events
kubectl describe pod <pod-name> -n <namespace>

# Check persistent volumes
kubectl get pv
kubectl get pvc -n <namespace>
```