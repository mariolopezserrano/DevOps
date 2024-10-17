1. Crear un rol llamado **pod-reader** que permita leer los logs de pods y containers del namespace **beebox-mobile**

```yaml
# pod-reader-role.yaml

apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: beebox-mobile
rules:
- apiGroups: [""]
  resources: ["pods", "pods/logs"]
  verbs: ["get", "list", "watch"]
```

2. Crear un RoleBinding para dar al usuario dev los permisos correspondientes.

```yaml
# pod-reader-role-binding.yaml

apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-reader-role-binding
  namespace: beebox-mobile
subjects:
- kind: User
  name: dev
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```