1. Crea un pod que exponga cada 5 segundos datos al host en el directorio /var/data usando un volumen.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-pod
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
    hostPath:
      path: /var/data
```

2. Crea un pod con mútiples contenedores que compartan datos usando volúmenes.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-volume-pod
  namespace: beebox
spec:
  containers:
  - name: busybox-output
    image: busybox
    volumeMounts:
    - name: data
      mountPath: /output
    command: ["/bin/bash"]
    args: ["-c", "cd output; while true; do echo hola >> data.txt; sleep 5; done;"]
  - name: busybox-input
    image: busybox
    volumeMounts:
    - name: data
      mountPath: /input
    command: ["/bin/bash"]
    args: ["-c", "cd input; while true; do cat data.txt >> new-data.txt; sleep 5; done;"]
  volumes:
  - name: data
    hostPath:
      path: /var/data-shared
```