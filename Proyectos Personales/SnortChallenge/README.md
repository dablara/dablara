# Write Up Snort Challenge- The Basics TryHackMe
 ## Índice
   - [Preámbulo](#preámbulo)
   - [Escenario](#escenario)
   - [Reto 1 - Analizando Trafico HTTP](#reto-1---analizando-trafico-http)
     - [Pregunta 1 Reto 1](#pregunta-1-reto-1)
     - [Pregunta 2 Reto 1](#pregunta-2-reto-1)
     - [Pregunta 3 Reto 1](#pregunta-3-reto-1)
     - Pregunta 4 Reto 1
     - Pregunta 5 Reto 1
     - Pregunta 6 Reto 1 
     - Pregunta 7 Reto 1 
     - Conclusión Primer reto
## Preámbulo
El análisis de tráfico de red en tiempo real es una habilidad esencial en ciberseguridad.
Snort, como sistema de detección de intrusos (IDS), permite monitorear, registrar y
analizar paquetes de red utilizando reglas personalizadas.
Este documento técnico tiene los siguientes objetivos:
 * Aprender los fundamentos del funcionamiento básico de Snort.
 * Comprender el proceso de captura de tráfico de red.
 * Aprender y practicar el uso de reglas de Snort para analizar   tráfico en tiempo
 real.
## Escenario
El escenario que TryHackMe nos presenta consiste en una máquina basada en Linux y
varios archivos que contienen comunicaciones de diferentes protocolos de red.
Mediante la creación y aplicación de reglas, y utilizando Snort como sistema de detección y análisis, podremos inspeccionar y analizar ese tráfico en tiempo real para identificar eventos relevantes y entender el comportamiento de la red.

![Escenario](imagenes/escenario.png)
## Reto 1 - Analizando Trafico HTTP
En este primer reto se nos presentan dos archivos: un archivo .pcap, que contiene los datos capturados del tráfico de red, y un archivo de reglas locales (“local.rules”), en el cual escribiremos las reglas necesarias para analizar dicho tráfico utilizando Snort

![Reto 1](imagenes/reto1.png)

La primera tarea del reto consiste en escribir una regla que permita detectar todo el tráfico TCP que se origine desde o se dirija hacia el puerto 80.

![Regla Puerto 80](imagenes/puerto80.png)

Una vez escrita, usaremos el archivo para detectar el tráfico dentro del archivo “.pcap”, con el uso del siguiente comando

Ejecutamos `sudo snort -c local.rules -A full -l . -r mx-3.pcap` para analizar el archivo pcap.

Este comando ejecuta Snort utilizando las reglas definidas en el archivo local.rules (-c),
en modo de alerta detallada (-A full), guardando la salida en el directorio actual (-l .) y analizando el archivo de captura mx-3.pcap (-r). 

Gracias a esto, podremos responder las siguientes preguntas que el reto nos presenta. 

Una vez ejecutado el comando, se mostrará un resumen del tráfico recogido, como se observa en la siguiente imagen:

![Ejecucion Comando](imagenes/ejecucioncomando.png)

Después de la ejecución, se generará un archivo de logs, el cual tendremos que analizar, ya que contendrá la información relevante para continuar con el reto.

### Pregunta 1 Reto 1
La primera pregunta del reto nos presenta, lo siguiente.

![Pregunta 1 Reto 1](imagenes/p1r1.png)

La pregunta nos dice lo siguiente: “¿Cuál es el número de paquetes detectados?”

Con la ejecución del comando anterior `sudo snort -c local.rules -A full -l . -r mx-3.pcap`, obtendremos la respuesta, si  analizamos la información ofrecida por el comando, sabemos que el número de paquetes es 164.

![Respuesta1](imagenes/r1p1.png)

## Pregunta 2 Reto 1
La segunda pregunta del reto es la siguiente

![Paquete63](imagenes/9a.png)

Dicha pregunta, nos pide “¿Cuál es la dirección de destino del paquete 63?.

Con el uso de comandos Snort, analizamos el documento de logs y especificamos que nos muestre lo referente al paquete 63.

![Paquete63a](imagenes/9.png)

La salida del comando es una seria de información, en este caso del paquete 63

Analizando el contenido nos damos cuenta de que se nos presenta información referente a las conexiones en el puerto: dirección de origen,destino,TTL,etc.

Fijándonos en la IP “216.239.59.99”, nos damos cuenta de que esta es la respuesta correcta.

![Direccion63](imagenes/10.png)
## Pregunta 3 Reto 1

Ahora la pregunta que nos plantea es la siguiente

![ACK](imagenes/12.png)
La cual nos pide “¿Cuál es el numero ACK del paquete 64?”
El ACK number (Acknowledgment Number) es el valor que indica al otro extremo que los datos se han recibido correctamente.

Para conocer este número haremos uso nuevamente del archivo de logs obtuvimos en la primera pregunta.

Haremos uso del mismo comando que usamos para ver la información del paquete 63 pero en este caso será del paquete 64

`sudo snort -r snort.log.1759422256 -n 64`

La salida del cual será la información antes vista, en este caso buscaremos el número ACK.

Fijándonos en la información obtenida, sabemos que la respuesta es la siguiente.

![ACK2](imagenes/13.png)

## Pregunta 4 Reto 1
Siguiendo con el reto, nos presenta la siguiente pregunta

![SEQ1](imagenes/SEQ1.png)

La pregunta reza la siguiente: “¿Cuál es el número SEQ del paquete 65?”

El **SEQ number (Sequence Number)**