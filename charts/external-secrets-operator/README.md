# External Secrets Operator (ESO)

Head over to the official documentation: https://external-secrets.io/latest/introduction/getting-started/

## Installation
```bash
helm repo add external-secrets https://charts.external-secrets.io
```
```bash
helm install external-secrets \
external-secrets/external-secrets \
-n external-secrets \
--create-namespace \
--version 0.9.9
# --set installCRDs=false
```

## Configuring a GCP Secret Store
We have configured the target cluster with Workload Identity, creating an specific Service Account with Viewer permissions. More [options are available](https://external-secrets.io/latest/provider/google-secrets-manager/).

The main requirements relate to:
- Having `Secret Manager Secret Accessor` role
- Doing a binding of the GCP Service Account to the Kubernetes Service Account managed by ESO:
```bash
# bind a gcp sa with a k8s sa at a specific k8s namespace
gcloud iam service-accounts add-iam-policy-binding \
    $GCP_SERVICE_ACCOUNT@$PROJECT.iam.gserviceaccount.com \
    --member="serviceAccount:$PROJECT.svc.id.goog[$NAMESPACVE/$K8S_SERVICE_ACCOUNT]" \
    --role="roles/iam.workloadIdentityUser"
```