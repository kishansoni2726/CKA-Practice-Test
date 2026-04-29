# 🚀 Q1: Install ArgoCD Using Helm (Without CRDs)

---

## 📘 Question

Install ArgoCD in a Kubernetes cluster using Helm while ensuring CRDs are **not installed** (as they are already pre-installed).

### 📋 Requirements

- Add the official ArgoCD Helm repository with name `argoCD`  
- Generate Helm template from ArgoCD chart version `7.7.3`  
- Use namespace `argocd`  
- Ensure CRDs are not installed  
- Save the generated YAML manifest to:


---

## ✅ Answer

### 1️⃣ Add ArgoCD Helm Repository

```bash
helm repo add argoCD https://argoproj.github.io/argo-helm
helm repo update

helm template argocd argoCD/argo-cd \
  --version 7.7.3 \
  --namespace argocd \
  --set crds.install=false \
  > /home/argo/argo-helm.yaml
