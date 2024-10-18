# Managing application configuration

Cuando se levantan aplicaciones en un clúster de kubernetes, con total seguridad deberás pasar, de forma dinámica, valores a tus aplicaciones para controlar su comportamiento. Esto se conoce como **application configuration**.

### Configmaps

Los configmaps son objetos de kubernetes que almacenan datos en forma de un mapa de clave-valor.

```yaml
#  Example of configmap especification

apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  key1: value1
  key2: value2
  key3:
    subkey:
        morekeys: data
        evenmore: some more data
  key4: |
    multi
    line
    data
```

### Secrets

Los secretos son similares a los configmaps pero son utilizados para tratar datos sensibles como contraseñas. Son creados y usados de forma similiar a los configmaps.

```yaml
#  Example of secret especification

apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: user
  password: mypass
```

### Variables de entorno

Para pasar la información de los ConfigMaps y los Secretos a los contenedores se pueden usar las **variables de entorno**, las cuáles serán visibles durante el proceso de ejecución del contenedor.

```yaml
#  Example of ENV Pod definition
spec:
  containers:
  - ...
    env:
    - name: ENVVAR
      valueFrom:
        configMapKeyRef:
          name: my-configmap
          key: mykey
```

### Configuration Volumes

Los datos de configuración procedentes de ConfigMaps y Secrets también pueden ser pasados a los contenedores in forma de **mounted volumes**. Esto implica que los datos se disponibilizarán en forma de ficheros en el propio sistema de ficheros del contenedor.