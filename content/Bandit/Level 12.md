#### Concepto
Análisis forense de archivos y descompresión en cadena (_Matryoshka_). El desafío consiste en identificar tipos de datos binarios ocultos tras un volcado hexadecimal y múltiples algoritmos de compresión.
#### Comandos clave
- `mktemp -d` para crear un directorio en la carpeta `/tmp` del servidor anfitrión.
- `xxd -r`: Para revertir el volcado hexadecimal a binario.
- `file`: Para identificar el tipo de archivo real (ignorando la extensión).
- `gunzip`: Para descomprimir archivos `.gz`.
- `bzip2 -d`: Para descomprimir archivos `.bz2`.
- `tar -xf`: Para extraer archivos de un empaquetado `.tar`.
- `mv`: Fundamental para renombrar y añadir extensiones que los descompresores exigen.
#### Resolución
El proceso fue iterativo: revertí el hexadecimal con `xxd -r`, y luego usé `file` para "ver" qué había dentro. Fui pelando capas (Gzip, Bzip2, Tar) renombrando el archivo con la extensión correspondiente cada vez que `file` me indicaba un cambio de formato, hasta que el comando reportó `ASCII text`.
#### Aprendizaje
Aprendí que las extensiones en Linux son solo sugerencias; lo que manda es el contenido real (identificado por `file`). También reforcé el uso de `/tmp` para trabajar en entornos restringidos y la importancia de la precisión en las flags de descompresión.
#### Pass 13
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn