#### Concepto
**SETUID (Set User ID) Binaries**. Un mecanismo de Unix que permite a los usuarios ejecutar archivos con los privilegios del propietario del archivo. Es una herramienta poderosa pero peligrosa si no se configura bien (vulnerabilidad de escalada de privilegios).
#### Comandos clave
- `ls -l`: Para identificar el bit `s` en los permisos (`-rwsr-xr-x`).
- `./archivo [comando]`: Ejecución del binario wrapper.
#### Resolución
`ls -l`
Localicé el binario `bandit20-do` que pertenece al usuario `bandit20` y tiene el bit SETUID activo. 
`./bandit20-do cat /etc/bandit_pass/bandit20`
Utilicé este programa como "puente" para ejecutar el comando `cat` sobre el archivo de contraseñas del siguiente nivel, al cual yo no tenía acceso directo pero el dueño del binario sí.
#### Cómo sabía el directorio?
En los niveles anteriores de Bandit, siempre te dicen que las contraseñas están en `/etc/bandit_pass/banditX`. Es una convención del juego. Si fueras un hacker en un sistema real, tendrías que:
1. Leer el código fuente del programa (si pudieras).
2. Usar `strings bandit20-do` para ver qué rutas hay escritas adentro del binario.
3. Simplemente probar las rutas estándar por instinto.
#### Aprendizaje
Aprendí que los permisos en Linux no son solo "lectura, escritura y ejecución". Existen bits especiales como SETUID que permiten delegar autoridad de manera temporal. Entendí que si un binario SETUID permite ejecutar comandos arbitrarios, es un agujero de seguridad masivo.
#### Pass 20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

