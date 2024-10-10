# Volumes
Los volumes pueden ser configurados de forma relativamente sencilla dentro de la especificación de los Pods/containers.

- **volumes**: En la especificación del Pod, se debe especificar los *storage volumes* disponibles en el Pod. Se debe especificar el tipo y otras especificaciones que determinan donde y como los datos son almacenados.

- **volumeMounts**: En la especificación de los contenedores se debe referenciar el volumen especificado en la configuración del Pod y proveer un *mountPath* (localización del sistema de ficheros desde donde el contenedor puede acceder a los datos).

```
#  Example of pod especification

apiVersion: v1
kind: Pod
metadata:
  name: volume-pod
spec:
  containers:
  - name: busybox
    image: busybox
    volumeMounts:
    - name: my-volume
      mountPath: /output
  volumes:
  - name: my-volume
    hostPath:
      path: /data
```

Se puede usar los *volumeMounts* para montar datos en múltiples contenedores del mismo Pod. Esta es una forma de que múltiples contenedores interactuen unos con otros.

## Tipos comunes de Volumes

- **hostPath**: los datos se encuentran en un directorio específico de un nodo de k8s.
- **emptyDir**: Este directorio solo existirá en el nodo mientras exista el Pod.