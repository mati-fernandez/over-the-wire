#### Concepto
**Cronjobs & Insecure Temporary Files:** El uso de tareas automáticas que depositan información sensible en directorios de escritura global (como `/tmp`) con permisos excesivos.
#### Comandos clave
- `cat /etc/cron.d/[nombre]`: Para inspeccionar tareas programadas.
- `&> /dev/null`: Redirección total al agujero negro del sistema (silenciar salida).
#### Resolución
Investigué la configuración de `cron` en `/etc/cron.d/` y encontré una tarea programada para el usuario `bandit22`. El cron ejecutaba un script cada minuto. Al inspeccionar dicho script, descubrí que volcaba la contraseña del siguiente nivel en un archivo temporal dentro de `/tmp/` con permisos de lectura pública. Bastó con leer ese archivo temporal para obtener la credencial.
#### Aprendizaje
Aprendí a seguir el rastro de la automatización en Linux. Si un proceso tiene más privilegios que yo y corre un script, ese script es una superficie de ataque. También comprendí la sintaxis básica de los archivos crontab.
**Seguridad:** Este es un ejemplo de **Insecure File Permissions**. El administrador está guardando información sensible en una carpeta pública (`/tmp`).
#### Pass 22
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q