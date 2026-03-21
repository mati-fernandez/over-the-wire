#### Concepto
**SSH Non-interactive Shell / Command Execution**. Evasión de scripts de inicio (`.bashrc` / `.profile`) que fuerzan el cierre de sesión.
#### Comandos clave
`ssh [user]@[host] "[command]"`: Ejecuta un comando remoto sin iniciar una sesión interactiva.
#### Resolución
El servidor de `bandit18` cerraba la conexión inmediatamente al intentar un login normal ("Bye bye!"). Para evadir esto, utilicé SSH para ejecutar directamente el comando `cat readme` desde mi terminal local. Al no solicitar una shell interactiva, el script de "auto-exit" no llegó a bloquear mi lectura del archivo.
#### Aprendizaje
Aprendí que SSH no es solo para "entrar" a una computadora remota, sino que sirve como un túnel para ejecutar instrucciones aisladas. Esto es fundamental para la automatización de servidores y para saltarse restricciones de shell.
SSH tiene dos modos: **Interactivo** (te da una terminal para escribir) y **No interactivo** (ejecuta un comando, te devuelve el texto y corta). Al poner un comando entre comillas al final, SSH asume que solo querés el resultado de esa instrucción y se salta la carga completa de la "shell" que te estaba echando con el "Bye bye".
#### Pass 19
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
