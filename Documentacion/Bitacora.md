# 📖 Bitácora del proyecto

---

## 🗓️ 1° Día
- Instalación de las máquinas virtuales de **Ubuntu Server** en **VirtualBox**.  
- Algunos conflictos con la inicialización en VirtualBox.  
- Configuración de almacenamiento, red y memoria.

---

## 🗓️ 2° Día
- Investigación de cómo hacer un **clúster con Kubernetes**.  
- Problemas con los gestores de paquetes **apt** y **snap**.  
- Investigación de cómo implementar **Moodle**.

---

## 🗓️ 3° Día
- Investigación de cómo arreglar la **MV maestro** y sus **MV esclavos**, por medio de la llave y el IP de cada una.  
- Se investigaron errores al momento de instalar **calico.yaml** y la creación del **token** en la MV Maestro.

---

## 🗓️ 4° Día
- Intento de inicializar el clúster con `kubeadm init`, pero se presentan errores relacionados con **cgroup** y la compatibilidad del **kernel**.  
- Investigación sobre cómo modificar los parámetros del kernel para que Kubernetes funcione correctamente.  
- Intento de solución modificando el archivo `/etc/containerd/config.toml`, pero persisten los errores.  
- Reinstalación de **containerd** y **kubeadm**, pero los errores persisten.

---

## 🗓️ 5° Día
- Revisión completa de las direcciones IP asignadas a cada MV.  
- Se encuentra un **conflicto de IPs** por configuración manual.  
- Se corrige el conflicto, pero ahora el **nodo esclavo** no se une al clúster.  
- Revisión de puertos y reglas del **firewall**; se desactiva temporalmente el firewall en las máquinas, sin éxito.  
- Investigación de **logs de kubelet** para diagnosticar el problema.  
- Se detecta que el servicio **kubelet** no inicia correctamente por errores de conexión con el **API Server**.  
- Se agota el tiempo sin lograr la conexión exitosa entre nodos ni la implementación de **Moodle sobre Kubernetes**.

---
