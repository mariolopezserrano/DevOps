# Container Health
Kubernetes ofrece una serie de funcionalidades que permiten construir soluciones robustas como puede ser la habilidad de reiniciar automaticamente contenedores con problemas. Para realizar este tipo de acciones, k8s necesita ser capaz de determinar el estado de las aplicaciones. Este concepto se denomina **container health**.

## Liveness Probes
La propiedad **Liveness probes** permite determinar si un contenedor de aplicación se encuentra en un estado "saludable". Por defecto, k8s sólo considera que una aplicación está caída si el proceso del contenedor se detiene. Liveness probes permite customizar este mecanismo de detección para que sea más sofisticado.

## Startup Probes
La propiedada **Startup probes** es bastante similar a liveness probes, sin embargo, mientras esta última se ejecuta contastemente, startup probes se ejecuta en el momento en el que la aplicación se levanta y termina una vez que la aplicación haya levantado.
Generalmente se usa para determinar cuando una aplicación ha levantado correctamente y es muy útil para aplicaciones con largos tiempo de start up.

## Readiness Probes
La propiedad **Readiness probes** se usa para determinar cuando un contenedor esta preparado para aceptar sus request. Se puede usar para prevenir tráfico en los pods si aún se encuentran en proceso de start up.