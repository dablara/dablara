# Pi-hole en Raspberry Pi en contenedores Docker, Docker Compose y Portainer

**Autor**: Daniel Blanco Aranda  
**Descripción**: Guía rápida para la instalación de Pi-hole en Raspberry Pi en contenedores Docker, Docker Compose y Portainer.

---

## 🧾 Índice

1. [Preámbulo](#preámbulo)  
2. [Preparativos](#preparativos)  
3. [Instalación](#instalación)
   - [Actualizar el sistema](#actualizar-el-sistema)
   - [Instalar Docker](#instalar-docker)
   - [Instalar Docker Compose](#instalar-docker-compose)
   - [Instalar Portainer](#instalar-portainer)
   - [Instalar Pi-hole](#instalar-pi-hole)
4. [Gestión desde Portainer](#gestión-desde-portainer)  
5. [Miscelánea](#miscelánea)  
6. [Configuración DNS en los clientes](#configuración-dns-en-los-clientes)  
7. [Posibles errores](#posibles-errores)
8. [Licencia](#licencia)
9. [Contacto](#contacto)


---

## Preámbulo 

**Pi-hole** es una herramienta que actúa como bloqueador de anuncios y rastreadores a nivel de red. 

Filtra las solicitudes de dominios no deseados, funcionando como un servidor DNS, lo que permite mejorar la privacidad y eliminar la publicidad en todos los dispositivos conectados, sin necesidad de instalar software adicional en cada uno.

Se configura generalmente en tu router, por lo que cualquier dispositivo que se conecte a tu red estará protegido de manera automática.

![Funcionamiento de Pi-Hole](https://github.com/dablara/dablara/blob/main/Proyectos%20Personales/Pi-HoleRaspberryPi/Imagenes/fun_pihole.png)
*Figura 1: Funcionamiento Pi-Hole*

---

En esta guía se instalarán también las siguientes herramientas:

- **Docker**: para contenerizar aplicaciones.
- **Docker Compose**: para gestionar servicios mediante un solo archivo.
- **Portainer**: una interfaz gráfica que facilita el control de contenedores.

 Portainer permite administrar contenedores existentes, crear nuevos, extraer imágenes y gestionar volúmenes y redes de forma sencilla.

---

##  Preparativos

Necesitaremos:

- Raspberry Pi 4 o 5 (recomendado)
- Tarjeta SD (16–32 GB) o almacenamiento externo
- Conexión Ethernet
- Sistema operativo Linux (sin entorno gráfico, opcional)

---

##  Instalación

###  Actualizar el sistema

```bash
sudo apt update && sudo apt upgrade -y
```

---

### Instalar Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
sudo usermod -aG docker <tu_usuario>
```
*Reemplaza <tu_usuario>, por tu usuario real*

*Nota: cerrar sesión y volver a entrar para aplicar cambios de grupo.*

---

### Instalar Docker Compose

```bash
sudo apt install -y curl jq
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

---

### Instalar Portainer

```bash
docker volume create portainer_data

docker run -d -p 9000:9000 -p 8000:8000   --name portainer   --restart=always   -v /var/run/docker.sock:/var/run/docker.sock   -v portainer_data:/data   portainer/portainer-ce
```

Abre en navegador:  
`http://<IP_DE_LA_RASPBERRY>:9000`  
Crea usuario, accede al panel y selecciona “Live Connect” para ver los contenedores.

![Portainer](https://github.com/dablara/dablara/blob/main/Proyectos%20Personales/Pi-HoleRaspberryPi/Imagenes/portainer.png)
*Figura 2: Portainer*

---

### Instalar Pi-hole

Crear carpetas:

```bash
mkdir -p /opt/pihole/etc-pihole
mkdir -p /opt/pihole/etc-dnsmasq.d
cd /opt/pihole
```

Crear archivo `docker-compose.yml`:

```yaml
version: '3'

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    restart: unless-stopped
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "80:80"
    environment:
      TZ: 'Europe/Madrid'
      PIHOLE_INTERFACE: eth0
      DNSMASQ_LISTENING: all
      DNSMASQ_ALLOW_FROM: 0.0.0.0/0
    volumes:
      - /opt/pihole/etc-pihole:/etc/pihole
      - /opt/pihole/etc-dnsmasq.d:/etc/dnsmasq.d
    cap_add:
      - NET_ADMIN
    dns:
      - 1.1.1.1
      - 8.8.8.8
```

Iniciar contenedor:

```bash
sudo docker-compose -f /opt/pihole/docker-compose.yml up -d
```

Asignar contraseña de acceso:

```bash
docker exec -it pihole pihole setpassword
```

Accede a:  
`http://<IP_DE_LA_RASPBERRY>:80/admin`

---

##  Gestión desde Portainer

1. Accede a Portainer (`http://<IP>:9000`)
2. Conéctate a tu entorno Docker con “Live Connect”
3. Ve a la sección **Containers** para ver Pi-hole en ejecución

---

## Gestión desde Terminal

```bash
dietpi@DietPi:~$ docker ps | grep pihole
40e5ae284dec   pihole/pihole:latest   "start.sh"   5 months ago   Up 37 hours (healthy)
```

## Miscelánea

### Respecto al docker_compose.yml

Puedes usar ambas opciones 

🔌 ports:
Mapea puertos del contenedor al host.
Ejemplo: "53:53/udp" → El puerto 53 del host se conecta al 53 del contenedor.
✅ Permite más control y evita conflictos entre contenedores.

🌐 network_mode: host
El contenedor comparte la red del host directamente.
No necesitas mapear puertos: el contenedor usa los del host como si fuera nativo.
✅ Ideal para servicios como Pi-hole que requieren acceso completo a la red local.
⚠️ Menor aislamiento: puede haber conflictos de puertos o riesgos de seguridad.

---

## 📡 Configuración DNS en los clientes:
DNS primario: <IP_DE_LA_RASPBERRY>

DNS secundario: 1.1.1.1 (Cloudflare) u otro de tu preferencia

(Opcional) También puedes configurar los DNS directamente en tu router de esta forma toda tu red estara protegida.

Aqui se muestra una vista de Pi-Hole, ya instalado y con tres clientes

![pihole](https://github.com/dablara/dablara/blob/main/Proyectos%20Personales/Pi-HoleRaspberryPi/Imagenes/piholevista.png)
*Figura 3: Pi-Hole ya montado.*

---
## Añadir Listas de Bloqueo
Puedes encontrar en internet múltiples listas que te ayudarán a bloquear anuncios, rastreadores y demás. 
Solo debes agregar la URL y seleccionar 'Add Blocklist'
![bloquear](https://github.com/dablara/dablara/blob/main/Proyectos%20Personales/Pi-HoleRaspberryPi/Imagenes/block.png)
*Figura 4: Añadir Listas de Bloqueo*

Despues de hacer esto debes dirigirte a Tools-->Update Gravity para actulizar la lista 

![Update](https://github.com/dablara/dablara/blob/main/Proyectos%20Personales/Pi-HoleRaspberryPi/Imagenes/up.png)
*Figura 5: Actulizar la lista de bloqueo*

Finalmente Pi-Hole, empezara a realizar su trabajo.


### Es posible que algunos anuncios de ciertas páginas no se bloqueen porque estos se cargan desde los mismos dominios que el contenido principal, lo que impide que Pi-hole los bloquee sin afectar el funcionamiento del sitio.

## Posibles errores

Uno de los principales errores que nos podríamos encontrar es el siguiente: 

**Los clientes no puedan resolver nombres DNS a través de Pi-hole.**

Esto suele ocurrir cuando el contenedor no está correctamente expuesto a la red, especialmente en el puerto 53 (DNS).

Estas dos opciones pueden solucionarlo.

 Opción 1: Exponer puertos manualmente
````bash
ports:
  - "53:53/tcp"
  - "53:53/udp"
  - "80:80"
````

Asegúrate de que ningún otro servicio esté usando esos puertos en el host.

Funciona bien si quieres que el contenedor esté aislado y solo use puertos específicos.

 Opción 2: Usar network_mode: host
```bash
network_mode: host
````
- Evita problemas de red relacionados con DNS.
- Ideal para casos donde Pi-hole debe actuar como servidor DNS de toda la red.
- No necesitas definir los puertos manualmente.

Una recomendacion es que si vas a usar Pi-hole y ningún otro contenedor que use el puerto 53 o 80, use la segunda opción.

##  Licencia

Este proyecto puede ser compartido y adaptado.

---

*Contribuciones y sugerencias bienvenidas.*

---
