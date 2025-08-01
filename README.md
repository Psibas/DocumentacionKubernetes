# DocumentacionKubernetes
Manual de instalación de Kubernetes con kubeadm (con explicación de comandos y errores comunes)
Este manual documenta detalladamente los pasos realizados, errores encontrados, imágenes de referencia y posibles mejoras durante la instalación de un clúster Kubernetes con kubeadm en un entorno Ubuntu. Se incluyen explicaciones técnicas de cada comando, los errores corregidos y una reflexión final sobre lo que se logró y lo que no.
________________________________________
Objetivo
Instalar y configurar un clúster de Kubernetes desde cero usando kubeadm, incluyendo la configuración del nodo maestro, instalación de red de pods y conexión de nodos trabajadores.
Requisitos previos
•	Ubuntu 20.04 o 22.04 (se recomienda evitar versiones no LTS).
•	Conexión a internet estable.
•	Acceso root o sudo.
•	Al menos 2 CPUs por nodo.
________________________________________
1. Actualización del sistema
sudo apt update && sudo apt upgrade -y
¿Qué hace?
Actualiza la lista de paquetes disponibles y aplica todas las actualizaciones pendientes del sistema operativo. El -y aprueba automáticamente las instalaciones sin pedir confirmación.
________________________________________
2. Error de repositorio
Mensaje:
E: El repositorio «https://apt.kubernetes.io kubernetes-xenial Release» no tiene un fichero de Publicación.
Causa: Estás usando una versión de Ubuntu no soportada por el repositorio Kubernetes.
Solución: Cambiar xenial por la versión correcta o usar una versión LTS soportada.
________________________________________
3. Edición del archivo /etc/fstab
sudo nano /etc/fstab
¿Qué hace?
Abre el archivo que define cómo montar las particiones. Se modificó para solucionar problemas de montaje.
Para guardar en nano:
•	Ctrl + O: Guardar
•	Enter: Confirmar
•	Ctrl + X: Salir
________________________________________
4. Teclado americano y símbolo ^
Solución para escribir ^: Presionar Shift + 6.
________________________________________
5. Error kubeadm: command not found
sudo apt install -y kubeadm
¿Qué hace?
Instala kubeadm, la herramienta principal para inicializar clústeres de Kubernetes.
________________________________________
6. Inicialización del clúster
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
¿Qué hace?
Inicializa el clúster de Kubernetes y configura el nodo como maestro. El parámetro --pod-network-cidr se usa para configurar la red de pods.
Errores comunes:
•	CPU insuficiente
•	kubelet no instalado o activo
•	No se genera admin.conf
Soluciones:
•	Asignar más CPUs a la VM.
•	Instalar y habilitar kubelet:
sudo apt install -y kubelet
sudo systemctl enable kubelet && sudo systemctl start kubelet
________________________________________
7. Archivo de configuración kubeconfig
mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
¿Qué hace?
Copia el archivo de configuración generado al directorio del usuario para que kubectl pueda comunicarse con el clúster.
________________________________________
8. Instalación de red de pods (Flannel)
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
¿Qué hace? Instala Flannel, un complemento de red que permite la comunicación entre pods distribuidos.
________________________________________
9. Agregar nodos al clúster
sudo kubeadm join <IP-MASTER>:<PORT> --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
¿Qué hace? Conecta un nodo trabajador al clúster principal.
________________________________________
Lo que se logró
•	Instalación completa de kubeadm, kubelet y kubectl.
•	Inicialización del clúster en el nodo maestro.
•	Instalación exitosa de red de pods (Flannel).
•	Corrección de errores comunes como falta de CPU, fallo de repositorio y permisos de archivos.


Lo que no se logró 
•	Conectar nodos trabajadores (no se completó por falta de entorno multi-nodo).
•	Requiere revisar compatibilidad de hardware virtual.
•	Sugerido usar herramientas como Minikube para entornos de prueba.
________________________________________________
Aspectos que no se lograron completar del todo

 El nodo maestro no tuvo nodos trabajadores unidos:
Faltó: Ejecutar el comando kubeadm join desde otro nodo para integrarlo al clúster.

Razón: No se configuraron múltiples nodos (por ejemplo, otras VMs o PCs).

Falta de pruebas de despliegue de pods:
No se verificó: Desplegar un pod de prueba y hacer kubectl get pods -A para validar funcionamiento.

Recomendación: Crear un pod de ejemplo para verificar que la red y la configuración estén correctas.

No se instalaron herramientas como metrics-server o dashboard:
Motivo: Enfocados en solucionar la base, no se alcanzó a implementar herramientas de monitoreo o UI.
________________________________________________
Errores Identificados y Soluciones Aplicadas

1.1 Repositorio de Kubernetes no válido
Error presentado:
E: El repositorio «https://apt.kubernetes.io kubernetes-xenial Release» no tiene un fichero de Publicación.

Causa: Se utilizó el nombre de versión de Ubuntu "xenial", el cual no es compatible con las versiones actuales del repositorio oficial.

Solución: Se reemplazó "xenial" por una versión LTS soportada, como "focal" (Ubuntu 20.04) o "jammy" (Ubuntu 22.04), en el archivo de repositorio correspondiente.

1.2 Comando kubeadm no encontrado
Error presentado:
kubeadm: command not found

Causa: La herramienta kubeadm no estaba instalada.

Solución: Se instaló utilizando el siguiente comando:

sudo apt install -y kubeadm

1.3 Fallo durante la inicialización con kubeadm
Errores presentados:

[ERROR NumCPU]: the number of available CPUs is less than the required 2
[ERROR KubeletVersion]: couldn't get kubelet version

Causa:

El sistema tenía asignada solo una CPU, cuando kubeadm requiere al menos dos.

El servicio kubelet no estaba habilitado ni instalado correctamente.

Solución:

Se incrementó el número de CPUs asignadas a la máquina virtual.

Se instalaron y habilitaron los servicios correspondientes:

sudo apt install -y kubelet
sudo systemctl enable kubelet
sudo systemctl start kubelet

1.4 Archivo de configuración no encontrado al copiar admin.conf
Error presentado:

cp: cannot stat '/etc/kubernetes/admin.conf': No such file or directory

Causa: El archivo no se generó debido a un fallo previo en la ejecución de kubeadm init.

Solución: Una vez corregido el fallo de inicialización, el archivo fue generado correctamente y copiado con:

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

1.5 Falta de red de pods

Problema: El clúster no contaba con una red de pods configurada, lo cual impedía la comunicación entre los mismos.

Solución: Se implementó la red Flannel mediante:

kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

1.6 Dificultad para ingresar símbolos en el teclado

Problema presentado: Imposibilidad de escribir el símbolo ^ en teclado con distribución estadounidense.

Solución: Se indicó la combinación correcta: Shift + 6.
