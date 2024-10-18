### **Guía de Comandos Básico de Linux para Administradores**
  

---
![imagen](/img/linux.jpg)

**1\. [Actualización y Mantenimiento del Sistema](actualizacion.md)**  
**2\. [Información del Sistema](informacion.md)**  
**3\. [Herramientas de Red](herramientas.md)**  
**4\. [Administración de Procesos](administracion.md)**  
**5\. [Gestión de Usuarios](gestion.md)**  
**6\. [Logs y Diagnósticos del Sistema](logs.md)**  
**7\. [Gestión de Paquetes](paquetes.md)**  
**8\. [Configuración de Redes](redes.md)**  
**9\. [Configuración de SSH](ssh.md)**  

---


#### **1\. Actualización y Mantenimiento del Sistema**

- **Actualizar el sistema:**  
  `sudo apt update`

  `sudo apt upgrade`

* *Descripción*: Actualiza la lista de paquetes y luego actualiza todos los paquetes instalados.  
    
- **Cambiar el nombre del host (hostname):**  
  `sudo nano /etc/hostname`  
  * *Descripción*: Edita el archivo del sistema para cambiar el nombre de la máquina.  
      
- **Cambiar la contraseña del usuario actual:**  
  `sudo passwd`  
    
- **Ver los repositorios configurados:**

  `sudo cat /etc/apt/sources.list.d/ubuntu.sources`  
  * *Descripción*: Muestra los repositorios configurados en el sistema para la instalación de paquetes.

---

#### **2\. Información del Sistema**

- **Ver versión del sistema operativo:**

  ```lsb_release -a```

- **Ver los paquetes instalados en la máquina:**

  `dpkg -l`

- **Ver la versión del núcleo (kernel):**

  `uname -a`  
    
- **Ver versión del entorno de escritorio:**

  `gnome-shell --version`  
    
- **Memoria libre disponible:**

  `free -h`  
    
- **Estado de la CPU:**  
    
  `lscpu`  
    
- **Ver el espacio en disco duro:**  
    
  `df -h`  
    
- **Ver los discos disponibles en el sistema:**  
  `lsblk`  
    
- **Datos de la red (configuración de interfaces):**  
  `ip a`  
    
- **Comprobar conectividad (ping):**  
  `ping google.es`

`ping -c 4 google.es`

- **Ver tabla de enrutamiento:**  
  `ip r`

---

#### **3\. Herramientas de Red**

**Ver puertos abiertos y conexiones:**  
`netstat -plunt`  
**Consultar DNS:**  
`sudo nslookup google.es`  
**Ver configuración de DNS locales:**  
`sudo nano /etc/hosts`

**Liberar configuración de red:**  
`sudo ip a flush “nombre_tarjeta_red”`

**Solicitar una nueva IP:**  
`sudo dhclient -v -s "IP_servidor"`

---

#### **4\. Administración de Procesos**

**Mostrar todos los procesos:**  
`ps aux`

**Matar un proceso específico:**  
`kill -9 “número_proceso”`

**Ver procesos en tiempo real:**  
`top`  
`htop`

**Cambiar a terminal textual (sin entorno gráfico):**  
`Ctrl + Alt + F3`

**Reiniciar entorno gráfico en caso de bloqueo:**

Cambiar a terminal textual con `Ctrl + Alt + F3`.

Ver el proceso del entorno gráfico con:  
`ps aux | grep gdm3`

Reiniciar el entorno gráfico:  
`sudo systemctl restart gdm3`

---

#### **5\. Gestión de Usuarios**

**Ver todos los usuarios del sistema:**  
`getent passwd`

**Ver contraseñas cifradas de los usuarios:**  
`getent shadow`

---

#### **6\. Logs y Diagnósticos del Sistema**

**Ver el registro del sistema:**

`sudo cat /var/log/syslog`

**Ver los eventos del arranque del hardware:**  
`dmesg`

**Ver los controladores (drivers) activos:**  
`lsmod`

---

#### **7\. Gestión de Paquetes**

**Desinstalar un paquete:**  
`sudo apt purge "nombre_paquete"`

**Comprobar si un paquete está instalado (ej. wget):**  
`apt policy wget`

---

#### **8\. Configuración de Redes**

##### **→ Debian:**

**Archivo de configuración de interfaces y DNS:**  
`sudo nano /etc/network/interfaces`

**Reiniciar servicio de red:**  
`sudo systemctl restart networking.service`

**Activar tarjeta de red:**  
`sudo ifup "nombre_tarjeta_red"`

**Desactivar tarjeta de red:**  
`sudo ifdown "nombre_tarjeta_red"`

##### 

##### **→ Ubuntu:**

**Archivo de configuración de red (Netplan):**  
`sudo nano /etc/netplan/01-netcfg.yaml`

**Aplicar cambios en la red:**  
`sudo netplan apply`

**Comprobar cambios en la red:**  
`ip a`  
`ip r`

**Estado de los DNS:**  
`resolvectl status "nombre_red"`

---

#### **9\. Configuración de SSH**

* **Permitir acceso como root vía SSH:**  
    
1. Editar el archivo de configuración de SSH:  
   `sudo nano /etc/ssh/sshd_config`  
2. Buscar la línea `PermitRootLogin` y cambiar su valor a:  
   `PermitRootLogin yes`  
3. Reiniciar el servicio de SSH:  
   `sudo systemctl restart ssh`

* **Crear claves SSH:**  
1. Generar un par de claves:  
   `ssh-keygen`  
     
1. Mover la clave pública al servidor remoto (ejemplo):  
   `ssh-copy-id usuario@servidor_remoto`

* **Acceso SSH sin contraseña:** Una vez configuradas las claves SSH, podrás acceder al servidor sin que te solicite la contraseña:  
  `ssh usuario@servidor_remoto`

