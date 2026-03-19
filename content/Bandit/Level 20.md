#### Concepto
**Modelo Cliente-Servidor (Localhost):** Interacción entre dos procesos independientes que se comunican a través de puertos de red locales. **Sockets:** Uso de puntos finales de comunicación (IP:Puerto) para transferir datos de forma segura entre niveles de privilegio.
#### Comandos clave
- `nc -l -p [puerto] < [archivo]`: Crea un servidor (daemon) que entrega el contenido del archivo a quien se conecte.
- `./`suconnect` [puerto]`: [[Binarios#suconnect|suconnect]] es un cliente con SETUID que valida la contraseña del nivel actual para entregar la siguiente.
- Si hubiera usado una sola terminal:
	- `&`: Ejecutar en segundo plano.
	- `jobs`: Listar tareas en segundo plano.
	- `fg`: Traer tarea al frente.
	- `CTRL+Z`: Pausar proceso actual.
#### Resolución
Para este desafío, utilicé un enfoque de **doble sesión SSH** para separar las responsabilidades del sistema:
1. **Terminal Servidor:** Creé un archivo temporal con la contraseña del nivel 20 (`echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" > /tmp/p20`) y puse a `nc` a escuchar en el puerto 12345, redireccionando el archivo hacia el puerto: `nc -l -p 12345 < /tmp/p20`.
2. **Terminal Cliente:** En una segunda sesión paralela, ejecuté el binario `./suconnect 12345`. El binario conectó exitosamente al servidor `nc`, recibió la contraseña, la validó internamente (gracias a sus permisos SETUID) y me devolvió la credencial del [[Level 21]].
>También se podía usar [[Job Control]] para gestionar el servidor en segundo plano y usar una sola terminal.
#### Aprendizaje
Aprendí que la comunicación entre procesos (IPC) mediante red es extremadamente útil cuando un programa necesita datos externos para realizar una validación de seguridad. También comprendí la diferencia operativa entre un proceso que "escucha" (servidor) y uno que "conecta" (cliente).

**Versión con una sola terminal:**
**IPC (Inter-Process Communication):** Aprendí que el "Job Control" de Linux permite gestionar procesos en segundo plano usando el símbolo `&`. Esto permite que un proceso actúe como servidor (daemon) mientras otro actúa como cliente en la misma sesión.
**[[Job Control]] y Background Processes**: Gestión de múltiples tareas en una sola shell interactiva.
#### Pass 21
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
