1. Modifica el Pod beebox-shipping-data situado en el namespace default configurando una restartPolicy cuando falle.

```yaml
```

2. Añadir la propiedad livenessProbe al contenedor para comprobar la respuesta de una petición http cada 5 segundos. La petición debe checkear la respuesta de la raíz (/) en el puerto 8080.
