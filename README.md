# argo-arc
Argo config for actions runner controller (arc) cluster

1. Install ArgoCD
1. Add creds. Settings > Repositories > Connect Repo > Via HTTPS, RepoUrl: https://github.com > Save as Credentials Template
1. Applications > New App (or kubectl apply a manifest):
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: bootstrap
  namespace: argocd
spec:
  project: default
  source:
    path: azure-east/bootstrap
    repoURL: https://github.com/jcantosz/argo-arc
    targetRevision: HEAD
  destination:
    namespace: argocd
    server: https://kubernetes.default.svc
  syncPolicy:
    automated:
      prune: true
```
1. Create github app, create secrets in k8s, create runner definitions
