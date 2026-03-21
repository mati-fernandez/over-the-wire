#### Acceso
Para este nivel no se utiliza una contraseña de texto, sino una **llave privada RSA** obtenida en el nivel anterior.
- **Comando de conexión:** `ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220`
#### Concepto
**Comparación de archivos (File Diffing)**. Identificación de cambios entre versiones de un mismo conjunto de datos. Fundamental para análisis forense o revisión de configuraciones.
#### Comandos clave
- `diff [archivo1] [archivo2]`: Compara archivos línea a línea.
- `cat`: Para verificar el contenido antes de comparar.
- `sort`: Útil si los archivos no están en el mismo orden (aunque en este nivel suelen estarlo).
#### Resolución
Al entrar al servidor con la llave RSA, encontré dos archivos: `passwords.old` y `passwords.new`. Utilicé `diff` para identificar qué línea había cambiado. El comando me señaló que la línea 42 fue modificada. La cadena marcada con `>` es la nueva contraseña.
#### Aprendizaje
Aprendí a leer la sintaxis de `diff`: el símbolo `<` representa el archivo origen y `>` el archivo destino. Esta herramienta es vital para no tener que buscar manualmente entre miles de líneas de texto similares.
#### Pass 
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
