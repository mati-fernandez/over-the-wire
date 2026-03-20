#### Concepto
**Insecure Cronjob Execution:** Escalada de privilegios mediante la ejecución automática de scripts en directorios con permisos de escritura para usuarios de menor rango.
#### Comandos clave
[[Bash Scripting#Analizando script del Level 23 de Over The Wire|Desglose del script encontrado]]
- **`mkdir /tmp/nombre`**: Crea un directorio temporal para trabajar.
- **`nano script.sh`**: Editor de texto simple para escribir el código del ataque.
- **`chmod 777`**: Otorga permisos totales (lectura, escritura, ejecución) para que el proceso de `bandit24` no falle al entrar o escribir.
- **`cp`**: Copia el script a la carpeta "caliente" que el cronjob vigila.
#### Resolución
Para este nivel, el objetivo fue "engañar" a un proceso automático que corre con privilegios de `bandit24`. Los pasos fueron:
1. **Reconocimiento:** Analicé el script `/usr/bin/cronjob_bandit24.sh` y descubrí que ejecuta cualquier archivo que me pertenezca dentro de `/var/spool/bandit24/foo` y luego lo borra.
2. **Preparación del Entorno:** Creé una carpeta en `/tmp/mi_ataque_23` y le di permisos `777`. Esto es crucial para que el usuario `bandit24` pueda escribir el resultado ahí adentro más tarde.
3. **Creación del Script Ladrón:** Usé `nano` para crear un archivo llamado `getpass.sh` con el siguiente contenido:
```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/mi_ataque_23/pass.txt
```
4. **Permisos de Ejecución:** Ejecuté `chmod 777 getpass.sh`. Sin este paso, el cronjob vería el archivo pero no tendría permiso para "correrlo".
5. **Inyección:** Copié mi script a la carpeta de ejecución: `cp getpass.sh /var/spool/bandit24/foo/`.
6. **Exfiltración:** Esperé un minuto a que el cronjob se activara. Una vez que el script original desapareció de la carpeta `foo`, revisé mi carpeta temporal y leí el archivo generado: `cat /tmp/mi_ataque_23/pass.txt`.
#### Aprendizaje
Aprendí que si un proceso con más poder que yo (`bandit24`) ejecuta mis scripts, puedo ordenarle que me entregue archivos a los que normalmente no tengo acceso (`/etc/bandit_pass/`). La clave fue asegurar que tanto mi **carpeta** como mi **script** tuvieran permisos `777` para evitar errores de acceso.
Este nivel te enseña que **"quien ejecuta el código"** es más importante que **"quien lo escribió"**. Al lograr que un usuario con más poder ejecute tu código, heredaste sus permisos por un segundo.
#### Pass 24
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
