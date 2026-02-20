# Write Up Snort Challenge- The Basics TryHackMe
 ## Índice
   - [Preámbulo](#preámbulo)
   - [Escenario](#escenario)
   - [Reto 1 - Analizando Trafico HTTP](#reto-1---analizando-trafico-http)
     - [Pregunta 1 Reto 1]
     - Pregunta 2 Reto 1
     - Pregunta 3 Reto 1
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
Mediante la creación y aplicación de reglas, y utilizando Snort como sistema de
detección y análisis, podremos inspeccionar y analizar ese tráfico en tiempo real para
identificar eventos relevantes y entender el comportamiento de la red.

![Escenario](imagenes/escenario.png)
## Reto 1 - Analizando Trafico HTTP
En este primer reto se nos presentan dos archivos: un archivo .pcap, que contiene los
datos capturados del tráfico de red, y un archivo de reglas locales (“local.rules”), en el
cual escribiremos las reglas necesarias para analizar dicho tráfico utilizando Snort

![Reto 1](imagenes/reto1.png)
La primera tarea del reto consiste en escribir una regla que permita detectar todo el tráfico TCP que se origine desde o se dirija hacia el puerto 80.

![Regla Puerto 80](imagenes/puerto80.png)
Una vez escrita, usaremos el archivo para detectar el tráfico dentro del archivo “.pcap”, con el uso del siguiente comando

![Comando Snort](imagenes/comandosnort.png)