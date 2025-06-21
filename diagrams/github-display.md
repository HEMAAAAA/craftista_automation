# Display Animated Diagrams in GitHub

## Option 1: GitHub Pages (Recommended)

### Setup GitHub Pages:
1. Go to repository **Settings** → **Pages**
2. Select **Source**: Deploy from a branch
3. Choose **Branch**: main
4. **Folder**: / (root)
5. Click **Save**

### Access URL:
```
https://HEMAAAAA.github.io/craftista_automation/diagrams/animated-architecture.html
```

### Add to README:
```markdown
## 🎨 Interactive Architecture
[View Animated Diagrams](https://HEMAAAAA.github.io/craftista_automation/diagrams/animated-architecture.html)
```

## Option 2: HTML Preview Services

### HTMLPreview.github.io:
```
https://htmlpreview.github.io/?https://raw.githubusercontent.com/HEMAAAAA/craftista_automation/main/diagrams/animated-architecture.html
```

## Option 3: Convert to GIF

### Create animated GIF:
1. Open `animated-architecture.html` in browser
2. Use screen recording tool
3. Convert to GIF
4. Add to README:

```markdown
![Architecture Animation](diagrams/architecture-animation.gif)
```

## Option 4: Static Screenshots

### Capture each view and display in README:
```markdown
### CI/CD Pipeline
![Pipeline](diagrams/pipeline-view.png)

### Microservices
![Services](diagrams/microservices-view.png)

### Kubernetes
![K8s](diagrams/kubernetes-view.png)
```