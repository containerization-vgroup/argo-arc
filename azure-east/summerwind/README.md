# Summerwind ARC
Also known as ARC v1
Not supported by GitHub (use scale-set version)


- https://github.com/actions/actions-runner-controller/tree/master?tab=readme-ov-file#legacy-documentation
- https://github.com/actions/actions-runner-controller/blob/master/docs/quickstart.md



After setup create a GitHub app and create a secret in the summerwind-arc namespace like:
  - `kubectl create secret generic controller-manager --namespace=summerwind-runner-system --from-literal=github_app_id=123456 --from-literal=github_app_installation_id=654321 --from-literal=github_app_private_key="$(cat path/to/cert.pem)"`
Secret's property names are the same as ARC v2 secret names
