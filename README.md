# 🚀 GitOps Demo with Argo CD

This repository demonstrates a simple **GitOps workflow** using Kubernetes and Argo CD.

---

## 🧠 What This Project Shows

* Declarative Kubernetes deployment
* Git as the **single source of truth**
* Automated deployment using Argo CD
* Self-healing and easy rollback

---

## 🏗️ Project Structure

```
.
├── app/
│   ├── deployment.yaml
│   └── service.yaml
```

---

## ⚙️ Tech Stack

* Kubernetes
* Argo CD
* Git (GitHub or any Git provider)
* Nginx (sample app)

---

## 🚀 How It Works

1. Kubernetes manifests are stored in Git
2. Argo CD watches this repository
3. Any changes pushed to Git are automatically applied to the cluster

```
Git Repo → Argo CD → Kubernetes Cluster
```

---

## 📦 Application Details

This repo deploys a simple **Nginx application** using:

* Deployment (with configurable replicas)
* Service (ClusterIP)

---

## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
```

---

### 2. Create Argo CD Application

Using CLI:

```bash
argocd app create nginx-app \
  --repo https://github.com/YOUR_USERNAME/YOUR_REPO.git \
  --path app \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```

---

### 3. Sync the Application

```bash
argocd app sync nginx-app
```

---

### 4. Verify Deployment

```bash
kubectl get pods
kubectl get svc
```

---

## 🧪 Testing GitOps

### 🔹 Scale the App

Edit `deployment.yaml`:

```yaml
replicas: 2 → 4
```

Push changes:

```bash
git commit -am "scale app"
git push
```

Argo CD will automatically update the cluster.

---

### 🔹 Test Self-Healing

```bash
kubectl delete pod <pod-name>
```

The pod will be recreated automatically.

---

### 🔹 Test Rollback

```bash
git revert HEAD
git push
```

Argo CD restores the previous working state.

---

## 🔥 Key Concepts

* **Declarative Configuration** → Define desired state
* **Source of Truth** → Git repository
* **Reconciliation Loop** → Ensures cluster matches Git
* **Self-Healing** → Fixes drift automatically

---

## ⚠️ Notes

* Ensure Argo CD is installed and running
* Make sure your repo is accessible (public or properly authenticated)
* Sync may be manual unless auto-sync is enabled

---

## 🎯 Future Improvements

* Enable auto-sync
* Add Helm support
* Multi-environment setup (dev/staging/prod)
* CI pipeline integration
