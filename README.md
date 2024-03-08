# argo-arc
Argo config for actions runner controller (arc) cluster

1. [Install ArgoCD](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)
   1. Get the generated admin password `kubectl -n argocd get secret argocd-initial-admin-secret -ojsonpath={.data.password} | base64 --decode | pbcopy`
   1. Get access to the ArgoCD UI: `kubectl -n argocd port-forward svc/argocd-server 8080:80` (https://localhost:8080)
   1. Log in with `admin/<paste password from clipboard>`
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
  - `kubectl create secret generic pre-defined-secret --namespace=arc-runners --from-literal=github_app_id=123456 --from-literal=github_app_installation_id=654321 --from-literal=github_app_private_key='-----BEGIN CERTIFICATE-----*******'`
