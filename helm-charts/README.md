# Craftista Helm Charts

Helm charts for deploying Craftista microservices platform to Kubernetes.

## Quick Start

### Install Helm Chart
```bash
# Add to dev environment
helm install craftista-dev ./craftista -f craftista/values-dev.yaml -n dev --create-namespace

# Add to staging environment  
helm install craftista-staging ./craftista -f craftista/values-staging.yaml -n staging --create-namespace
```

### Upgrade Deployment
```bash
# Upgrade with new image tags
helm upgrade craftista-dev ./craftista -f craftista/values-dev.yaml -n dev --set global.imageTag=v1.2.3

# Upgrade staging
helm upgrade craftista-staging ./craftista -f craftista/values-staging.yaml -n staging --set global.imageTag=v1.2.3
```

## Chart Structure

```
craftista/
├── Chart.yaml              # Chart metadata
├── values.yaml             # Default values
├── values-dev.yaml         # Development overrides
├── values-staging.yaml     # Staging overrides
└── templates/
    ├── _helpers.tpl        # Template helpers
    ├── frontend.yaml       # Frontend service
    ├── catalogue.yaml      # Catalogue service
    ├── recommendation.yaml # Recommendation service
    ├── voting.yaml         # Voting service
    └── databases.yaml      # MongoDB & PostgreSQL
```

## Configuration

### Environment Values
- **values-dev.yaml** - Lower resources, single replicas
- **values-staging.yaml** - Higher resources, multiple replicas
- **values.yaml** - Base configuration

### Key Parameters
```yaml
global:
  imageTag: latest           # Override image tags
  imagePullPolicy: Always    # Image pull policy

frontend:
  enabled: true             # Enable/disable service
  replicaCount: 1          # Number of replicas
  service:
    type: LoadBalancer     # Service type
    port: 3000            # Service port
```

## ArgoCD Integration

### Update ArgoCD Applications
```yaml
# craftista-dev-app.yaml
spec:
  source:
    path: helm-charts/craftista
    helm:
      valueFiles:
        - values-dev.yaml
```

## Commands

### Development
```bash
# Install
helm install craftista-dev ./craftista -f craftista/values-dev.yaml -n dev --create-namespace

# Upgrade
helm upgrade craftista-dev ./craftista -f craftista/values-dev.yaml -n dev

# Uninstall
helm uninstall craftista-dev -n dev
```

### Staging
```bash
# Install
helm install craftista-staging ./craftista -f craftista/values-staging.yaml -n staging --create-namespace

# Upgrade
helm upgrade craftista-staging ./craftista -f craftista/values-staging.yaml -n staging

# Uninstall
helm uninstall craftista-staging -n staging
```

## Benefits Over Kustomize

### Advantages
- **Templating** - Dynamic configuration with Go templates
- **Versioning** - Built-in release management
- **Rollbacks** - Easy rollback to previous versions
- **Dependencies** - Manage chart dependencies
- **Packaging** - Distribute as packages

### Use Cases
- **Complex configurations** with many parameters
- **Multiple environments** with different settings
- **Version management** of deployments
- **Rollback capabilities** for production

## Helm vs Kustomize Comparison

| Feature | Helm | Kustomize |
|---------|------|-----------|
| Templating | ✅ Go templates | ❌ Overlay-based |
| Versioning | ✅ Built-in | ❌ Git-based only |
| Rollbacks | ✅ helm rollback | ❌ Manual |
| Complexity | Higher | Lower |
| Learning Curve | Steeper | Gentler |
| GitOps | ✅ Supported | ✅ Native |

Both approaches are valid - choose based on your team's needs and complexity requirements.