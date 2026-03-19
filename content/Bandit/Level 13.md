#### Concepto
Autenticación mediante **Llaves Privadas SSH** (Identity Files). El nivel exige mover la llave al entorno local porque el servidor bloquea el salto interno por `localhost`.
#### Comandos clave
- `scp -P 2220`: Para descargar archivos del servidor a la PC local.
- `ssh -i`: Para loguearse usando un archivo de identidad en lugar de password.
- **GUI de Windows (Seguridad)**: Para gestionar permisos NTFS (Deshabilitar herencia).
#### Resolución
`scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private .`
Descargué `sshkey.private` con `scp` (secure copy). Como Windows no procesa `chmod` igual que Linux, usé la **interfaz de Propiedades > Seguridad** del archivo para quitar la herencia y dejar solo a mi usuario con permisos de lectura. Luego, conecté desde mi terminal a `bandit14@bandit.labs.overthewire.org` por el puerto `2220`.
#### Aprendizaje
Aprendí que SSH rechaza llaves "expuestas" (con permisos compartidos). En Windows, esto se soluciona rompiendo la herencia de permisos en la GUI para que el archivo sea privado. También validé que el archivo `HINT` es clave cuando las reglas estándar del servidor cambian.
#### Pass 14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS