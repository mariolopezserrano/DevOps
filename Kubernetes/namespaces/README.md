# Namespaces
Los namespaces son clústeres virtuales que pertenecen al mismo clúster físico. Los objetos de kubernetes (pods, containers, etc) se sitúan dentro de namespaces. Realmente, se pueden considerar una forma de organizar y/o separar objetos en tu clúster de kubernetes.

Para listar los namespaces existentes se usa el siguiente comando:

```
kubectl get namespaces
```

Todos los clúster se tiene un namespace por defecto (default) que se usa cuando no se especifica otro. Kubeadm también crea otro namespace (kube-system) para alojar los componentes del sistema.

Cuando se usa kubectl debes especificar el namespace con el flag --namespace. Si no se especifica uno en concreto se asume default como namespace.

```
kubectl get pods --namespace my-namespace
```

```
# Obtener los pods de todos los namespaces
kubectl get pods --all-namespaces
```

También puedes crear un namespace usando kubectl:

```
kubectl create namespace my-namespace
```