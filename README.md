# 🐍 Python App Helm Chart

This repository hosts the Helm chart for deploying the **Python Web App** to Kubernetes clusters.  
The chart is packaged and served via **GitHub Pages**, allowing it to be added and installed using `helm repo add`.

---

## 🚀 Prerequisites

- Kubernetes cluster (e.g., AKS, Minikube, etc.)
- Helm 3.x installed
- Azure Container Registry (ACR) credentials (if using a private image)

---

## ⚙️ Setup Steps

### 1️⃣ Create Namespace & Registry Secret

```bash
kubectl create ns python-app

kubectl create secret docker-registry acr-secret \
  --docker-server=<acr-registry-name>.azurecr.io \
  --docker-username=<acr-username> \
  --docker-password=<acr-password> \
  --docker-email=<email> \
  -n python-app
```

### 2️⃣ Create & Configure Helm Chart

```bash
helm create python-app-chart
cd python-app-chart

```

### 3️⃣ Package the Chart

From the parent folder:
```bash
helm package python-app-chart
```

### 4️⃣ Create Helm Repo Index

```bash
helm repo index . --url https://<your-github-username>.github.io/<repo-name>
```

Example:
```bash
helm repo index . --url https://tajgithub24.github.io/python-webapp
```

### 5️⃣ Push Files to GitHub

```bash
git add .
git commit -m "Add Helm chart and index"
git push -u origin main
```

### 6️⃣ Enable GitHub Pages

* Go to your GitHub repo → Settings → Pages

* Select:

    * Branch: main

    * Folder: / (root)

* Click Save

Your Helm repo will be available at:

```bash
https://<your-username>.github.io/<repo-name>/index.yaml
```

Example:
```bash
https://tajgithub24.github.io/python-webapp/index.yaml
```

### 7️⃣ Verify Repo

Open the URL above in your browser.
You should see YAML output.

### 8️⃣ Add and Install Chart

```bash
helm repo add my-python-app https://tajgithub24.github.io/python-webapp/
helm repo update
helm install python-app my-python-app/python-app-chart -n python-app
```

### ✅ Validate Deployment
```bash
kubectl get all -n python-app
```

If the Service type is LoadBalancer, run:
```bash
kubectl get svc -n python-app
```
