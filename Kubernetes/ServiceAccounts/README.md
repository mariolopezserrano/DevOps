# Service Accounts
En kuberentes, un service account es una identidad usada por los procesos dentro de los pods para autenticarse con la API de k8s (es decir, para realizar acciones dentro del clúster).

Para manejar el control de acceso de los service accounts se usan objetos de tipo RBAC.

Los objetos RoleBinding y ClusterRoleBinding pueden ser usados para enlazar permisos a service accounts al igual que a usuarios o grupos de usuarios.

```yaml
# Ejemplo de RoleBinding para Service Account

apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: sa-pod-reader
subjects:
- kind: ServiceAccount
  name: my-serviceaccount
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io/v1
```