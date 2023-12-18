# Kubernetes Dashboard
A General purpose GUI for Kubernetes.

It can be used to view, but also to edit cluster resources. It is deployed on the target cluster itself, and authorization is going to default to `KUBECONFIG`.

## Installation
Refer to the [official Chart](https://artifacthub.io/packages/helm/k8s-dashboard/kubernetes-dashboard).

```bash
helm upgrade --install kubernetes-dashboard . -f values.yaml
```

## RBAC
The following will be created:

```yaml
# read-only-sa.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: read-only-user
  namespace: kubernetes-dashboard
```

```yaml
# read-only-cluster-role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: read-only-cluster-role
rules:
- apiGroups: ["*"]
  resources: ["*"]
  verbs: ["get", "list", "watch"]
- apiGroups: ["*"]
  resources: ["secrets"]
  verbs: ["deny"]
```

```yaml
# read-only-cluster-role-binding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-only-user-binding
subjects:
- kind: ServiceAccount
  name: read-only-user
  namespace: kubernetes-dashboard
roleRef:
  kind: ClusterRole
  name: read-only-cluster-role
  apiGroup: rbac.authorization.k8s.io
```