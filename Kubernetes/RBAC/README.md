# Role-Based Access Control (RBAC)
El control de acceso basado en roles (RBAC) en k8s permite controlar que usuarios acceden y que acciones pueden realizar los mismos en un clúster de kubernetes.

**Roles** y **ClusterRoles** son objetos de kuberentes que definen un conjunto de permisos que definen que acciones pueden realizar los usuarios dentro del clúster.

- **Role**: define permisos dentro de un namespace específico.
- **ClusterRole**: define permisos a nivel global dentro del clúster.

Los objetos **RoleBinding** y **ClusterRoleBinding** son objetos que conectas Roles y ClusterRoles con los usuarios o identidades.

```
# Ejemplo de Role

apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

- **apiGroups**: en esta sección se especifican los grupos de la API a los que se van a aplicar los permisos definidos.
    - **""/core**: API core de k8s (pods, services, configmaps, nodes).
    - **apps**: Incluye objetos como deployments, statefulset.
    - **batch**: Incluye objetos como jobs o cronjobs.
    - **rbac.authorization.k8s.io**: Incluye objetos RBAC.

- **verbs**: en esta sección se definen las acciones específicas que se pueden realizar con este role (sobre los recursos especificados).
    - **get**: Permite leer o recuperar recursos pero no modificarlos
    - **list**: Permite listar recursos.
    - **watch**: Permite observar los cambios en los recursos.
    - **create**: Permite crear nuevos recursos.
    - **update**: Permite modificar recursos existentes.
    - **patch**: Permite realizar modificaciones parciales en los recursos existentes.
    - **delete**: Permite eliminar recursos.
    - **deletecollection**: Permite eliminar múltipes recursos a la vez.