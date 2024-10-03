# Storage
Una de las principales características de los contenedores es que su sistema de ficheros es efímero. Es decir, estos ficheros únicamente existirán durante la vida del contenedor. Si un contenedor es recreado o eliminado los datos que se encuentran en su sistema de ficheros se perderán.

La mayoría de aplicaciones necesitan un método de persistencia de datos.

- Los **volumes** permiten almacenar datos fuera del sistema de ficheros del contenedor y permiten que los datos sean accesibles en tiempo de ejecución.

    - container -> external storage

- Los **persistent volumes** son significamente más avanzados que los volúmenes. Permiten tratar el almacenamiento como un recurso abstracto y que los pods accedan a ellos.

    - pod -> persisten volumen claim -> persistent volume -> external storage

## Tipos de volume

Tanto los Volumes como los Persisten Volumes tienen diferents volume types. Estos determinan como se maneja realmente el almacenamiento.

- NFS
- Mecanismos de almacenamientos en la nube
- Secretos y Configmaps
- Directorios en los nodos de kuberentes