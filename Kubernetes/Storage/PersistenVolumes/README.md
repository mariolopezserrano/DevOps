# PersistentVolumes
Los PersistentVolumes son objetos de kubernetes que permiten tratar el almacenamiento como recursos abstractos que consumen los Pods (como pueden ser los recursos de memoria y CPU).

```yaml
#  Example of PV especification

apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  storageClassName: localdisk
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /var/output
```

Los PersistentVolume poseen una serie de atributos usados para describir los recursos de almacenamiento subyacentes (por ejemplo, la localización de datos en la nube) los cuales son usados para almacenar los datos.

- **Storage Classes**
Los Storage Classes permiten a los administradores especificar los tipos de almacenamiento que ofecen en su plataforma. La propiedad **allowVolumeExpansion** permite definir si un Storage Class puede recalcular su capacidad una vez creado el recurso.

- **Reclaim Policy**
Esta propiedad de los PersistenVolume determina como los datos almacenados pueden ser reusados cuando el PersistentVolumeClaim asociado es eliminado.
  - **Retain**: Se mantienen todos los datos.
  - **Delete**: Elimina los datos subyacentes (solo funciona con recursos de almacenamiento en la nube).
  - **Recycle**: Elimina los datos pero mantiene el PersistenVolume para ser reusado.

# PersistentVolumeClaim
Un **PersistentVolumeClaim** representa una petición para los recursos de almacenamiento. Son necesarios una serie de atributos de forma similar que para los PersistentVolume.

```yaml
#  Example of PVC especification

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  storageClassName: localdisk
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 100Mi
```
Cuando un PVC es creado se busca un PV que cumpla con los criterios y automáticamente se enlazan.

Los PVC son montados en los Pods como cualquier otro tipo de volumen. Si el PVC está enlazado a un PV, el Pod usará el almacenamiento subyacente.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pv-pod
spec:
  containers:
  - name: busybox
    image: busybox
    volumeMounts:
    - name: pv-storage
      mountPath: /output
  volumes:
  - name: pv-storage
    persistentVolumeClaim:
      claimName: my-pvc
```

Es posible expandir el tamaño de petición de los PVC sin interrupción ni aceptación en las aplicaciones pero la propiedad **allowVolumeExpansion** debe ser true.