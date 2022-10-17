# Github Actions Autoscaler

We run an Azure Kubernetes Cluster.

On you host with set up kubectl:
```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.9.1/cert-manager.yaml
kubectl create -f https://github.com/actions-runner-controller/actions-runner-controller/releases/download/v0.26.0/actions-runner-controller.yaml
```

Then follow these instructions to get a Github Personal Access Token (or get it from Bitwarden): https://github.com/actions-runner-controller/actions-runner-controller/blob/master/docs/detailed-docs.md#deploying-using-pat-authentication

```bash
kubectl create secret generic controller-manager \
-n actions-runner-system \
--from-literal=github_token=${GITHUB_TOKEN}
```

Then apply the config:
```bash
kubectl apply -f .
```