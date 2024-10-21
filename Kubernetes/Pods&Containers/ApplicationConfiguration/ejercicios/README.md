1. Usar la herramienta htpasswd para generar un fichero htpasswd. Crear un secreto llamado nginx-htpasswd y guarda el contenido del fichero que se acaba de generar.

Para crear el fichero se debe usar el siguiente comando:
```
htpasswd -c .htpasswd user
```

Para crear el secreto nginx-htpasswd a partir del fichero anterior se debe lanzar el siguiente comando:
```
kubectl create secret generic nginx-htpasswd --from-file .htpasswd
```

2. Crear un pod con un solo contenedor que use la imagen nginx:1.19.1. La configuración correspondiente al Nginx está guardado en un ConfigMap existente llamado nginx-config. Monta el configmap anterior en la ruta /etc/nginx del Pod. Monta el secreto htpasswd en la ruta /etc/nginx/conf del Pod. Expon el containerPort al puerto 80 y realizar una prueba de comunicación para probar la configuración.

Se define la especificación del pod nginx con los requerimientos:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.19.1
    ports:
    - containerPort: 80
    volumeMounts:
    - name: config-volume
      mountPath: /etc/nginx
    - name: htpasswd-volume
      mountPath: /etc/nginx/conf
  volumes:
  - name: config-volume
    configMap:
      name: nginx-config
  - name: htpasswd-volume
    secret:
      secretName: nginx-htpasswd
```

Para realizar la prueba de conectividad/configuración se puede usar cualquier otro Pod mediante curl:

```
kubectl exec busybox -- curl -u user:<PASSWORD> <NGINX_POD_IP>
```