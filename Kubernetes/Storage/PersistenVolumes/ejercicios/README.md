1. Crear un PersistentVolume alojado en el host con un size de 1Gi que almacene datos en la ruta /var/output. Asegúrate que
el PersistenVolume es configurado para que los volúmenes del Pod pudieran ser expandidos. Adicionalmente, configura el
volumen para que sea reusable si su claim es eliminado.

En primer lugar hay que crear la storageclass:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: localdisk
provisioner: kubernetes.io/no-provisioner
allowVolumeExpansion: true
```
Seguidamente se crea el PV asociado a la storageclass anteriormente creada:

```yaml
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

2. Crea un PersistenVolumeClaim con un size de 100Mi. Asegúrate de que se enlaza con el PV creado anteriormente.

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
  namespace: beebox
spec:
  storageClassName: localdisk
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 100Mi
```

3. Crea un Pod que use ese PV como volumen.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod
  namespace: beebox
spec:
  containers:
  - name: busybox
    image: busybox
    volumeMounts:
    - name: data
      mountPath: /output
    command: ["/bin/sh"]
    args: ["-c", "cd output; while true; do echo hola >> data.txt; sleep 5; done;"]
  volumes:
  - name: data
    persistentVolumeClaim:
      claimName: my-pvc
```