**Análisis de Puertos (Reconocimiento)** Tras escanear el rango 31000-32000, se identificaron 5 puertos abiertos. La fase de enumeración manual reveló lo siguiente:
- `31046`: **Descartado**. No utiliza SSL (Error de handshake).
- `31518`: **Eco Server**. Habla SSL pero devuelve el mismo string enviado.
- `31691`: **Descartado**. Comportamiento similar a 31046.
- **`31790`**: **¡GANADOR!** Puerto SSL que, tras recibir la pass del L15, devuelve la credencial del L17.
- `31960`: **Descartado**. No responde a credenciales.
#### Concepto
**Escaneo y Enumeración de Servicios SSL**. El nivel combina el descubrimiento de puertos (`nmap`) con la interacción manual en servicios cifrados para extraer credenciales no triviales (llaves RSA).
#### Comandos clave
- `nmap -p 31000-32000 localhost`: Escaneo básico de puertos.
- `nmap -p 31000-32000 -sV localhost`: Escaneo con detección de versiones y servicios (no sirvió, se cuelga).
- `openssl s_client -connect localhost:31790 -ign_eof`: Conexión manual manteniendo el túnel abierto.
#### Resolución
- Ejecuté `nmap` para localizar puertos abiertos.
- Utilicé `openssl s_client` con la flag `-ign_eof` en el puerto `31790`.
- Envié la contraseña del Level 15.
- El servidor respondió con una **RSA Private Key**.
- Guardé la llave en `bandit17.key` y ajusté los permisos en Windows (Seguridad > Avanzado > Deshabilitar herencia) para poder usarla. Estableciendo permiso solo de lectura para mi usuario.
#### Aprendizaje
Aprendí que `nmap` es solo el primer paso; la **enumeración manual** es la que confirma cuál servicio es útil. También comprendí que los servidores pueden devolver diferentes tipos de credenciales, como llaves RSA, que requieren un manejo de archivos más cuidadoso que una simple contraseña de texto.
#### Pass 17
En este nivel no hay pass. Debemos ingresar al server bandit17 con el siguiente comando aprovechando la sshkey obtenida en el nivel 16. Para poder hacerlo en este caso, abrí la terminal en la misma carpeta que la llave.
`ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220`
[Llave RSA](bandit17.key)

