# Role-Based Access Control (RBAC)
El control de acceso basado en roles (RBAC) en k8s permite controlar que usuarios acceden y que acciones pueden realizar los mismos en un clúster de kubernetes.

**Roles** y **ClusterRoles** son objetos de kuberentes que definen un conjunto de permisos que definen que acciones pueden realizar los usuarios dentro del clúster.

- **Role**: define permisos dentro de un namespace específico.
- **ClusterRole**: define permisos a nivel global dentro del clúster.

Los objetos **RoleBinding** y **ClusterRoleBinding** son objetos que conectas Roles y ClusterRoles con los usuarios o identidades.