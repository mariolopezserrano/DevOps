# Restart Policies
Kubernetes ofrece la posibilidad de reinicirar contenedores cuando fallen. Las **Restart Policies** permiten customizar este comportamiento definiendo cuando los contenedores deben ser reiniciados automáticamente.
Las restart policies son un componente importante para las aplicaciones *self healing*, las cuales son automaticamente recuperadas cuando aparece alguna problemática.


Hay tres posibilidades para configurar las políticas de Restart Policie:

### Always
Always es la Restart Policy por defecto en kubernetes. Con esta política, los contenedores siempre serán reiniciados si son detenidos (incluso si han terminado los procesos satisfactoriamente). Esta política es de utilidad para aplicaciones que deberían estar siempre levantadas y en funcionamiento.

### OnFailure
La Restart Policy Onfailure reinicia los contenedores únicamente si existe algún error en el proceso de ejecución o si el liveness probe determina que la aplicación está unhealthy. Esta política es de utilidad para aplicaciones que deben ser ejecutadas y después parar.

### Never
La RestartPolicy Never implica que los contenedores de los Pods nunca se reinicien aunque los procesos terminen o la aplicación sea unhealthy. Esta política es útil para aplicaciones que se ejecutan una única vez y no deben ser reinicidadas de forma automática.