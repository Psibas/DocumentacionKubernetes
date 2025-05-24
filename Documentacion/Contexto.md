# Caso de estudio: Falta de infraestructura y capacitación para implementar laboratorios de informática prácticos en colegios rurales

## Contexto
En las zonas rurales del departamento de Cundinamarca, Colombia, un colegio enfrenta serias limitaciones tecnológicas que afectan la calidad de la educación. La falta de una plataforma local para desarrollar competencias digitales sin depender de internet, sumada a la escasa capacitación técnica del personal docente y a la obsolescencia de los equipos, impide incorporar contenidos actualizados en áreas clave como redes, cloud computing o desarrollo de software. Esto genera una brecha en la formación de los estudiantes y limita su capacidad para desarrollar habilidades técnicas alineadas con el mundo laboral.

## A. Diagnóstico
- Conectividad intermitente o nula, que limita el uso de plataformas educativas en línea.
- Equipos de bajo rendimiento que impiden la instalación de software moderno o la ejecución de entornos virtuales.
- Ausencia de recursos tecnológicos locales para realizar prácticas en tecnologías emergentes.
- Se propone implementar un entorno local de aprendizaje basado en Kubernetes en una red LAN educativa, usando máquinas virtuales con Ubuntu Server y kubeadm o Minikube, para simular prácticas reales de orquestación y despliegue de servicios sin necesidad de internet.
![Topología del clúster Kubernetes](ola%20(1).jpg)

## B. Tecnologías a Usar
- **Ubuntu Server**: sistema operativo base para todos los nodos del clúster, elegido por su estabilidad, compatibilidad con Kubernetes, bajo consumo de recursos y amplia documentación.
- **Kubernetes (kubeadm)**: plataforma de orquestación de contenedores para administrar y desplegar aplicaciones distribuidas, con funcionalidades como escalado, balanceo de carga y recuperación ante fallos.
- **Horizontal Pod Autoscaler (HPA)**: ajusta automáticamente el número de réplicas según métricas como el uso del CPU.
- **GitHub**: repositorio donde se alojará el código, configuraciones, scripts y documentación del proyecto.

## C. Diagnóstico Plan de formación y despliegue
### Infraestructura
- Montaje de un clúster Kubernetes local usando máquinas virtuales Ubuntu Server.
- Uso de kubeadm para instalación y configuración del clúster con nodos master y worker.
- Configuración de red LAN para comunicación interna.
### Formación técnica
- Capacitación a docentes en administración de sistemas Linux, Kubernetes y clústeres.
### Material didáctico
- Documentación detallada de instalación y uso.
- Scripts automatizados para despliegue de servicios.
### Despliegue
- Instalación física y virtual del clúster.
- Pruebas de despliegue y escalado automático.
- Integración de monitoreo para evaluar desempeño.

## D. Métricas de impacto
- **Participación**: porcentaje de docentes y estudiantes que acceden al sistema e interactúan con los componentes educativos.
- **Competencias adquiridas**: evaluación práctica de habilidades para desplegar y administrar contenedores en Kubernetes.
- **Disponibilidad**: tiempo de actividad del clúster y estabilidad operativa.
- **Tiempo en uso**: duración en la que estudiantes y docentes pueden interactuar académicamente con el clúster sin fallas operativas.

