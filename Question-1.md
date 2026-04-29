Q1: Install ArgoCD Using Helm (Without CRDs)
📘 Question

Install ArgoCD in a Kubernetes cluster using Helm while ensuring CRDs are not installed (as they are already pre-installed).

Requirements:
Add the official ArgoCD Helm repository with name argoCD
Generate Helm template from ArgoCD chart version 7.7.3
Use namespace argocd
Ensure CRDs are not installed
Save the generated YAML manifest to /home/argo/argo-helm.yaml


✅ Answer
1. Add ArgoCD Helm Repository
helm repo add argoCD https://argoproj.github.io/argo-helm
helm repo update
2. Generate Helm Template (Skip CRDs)
helm template argocd argoCD/argo-cd \
  --version 7.7.3 \
  --namespace argocd \
  --set crds.install=false \
  > /home/argo/argo-helm.yaml
📂 Output

The generated manifest will be available at:

/home/argo/argo-helm.yaml
📝 Notes
--set crds.install=false ensures CRDs are not installed
helm template only generates YAML (does not deploy)
To apply manifests:
kubectl apply -f /home/argo/argo-helm.yaml
