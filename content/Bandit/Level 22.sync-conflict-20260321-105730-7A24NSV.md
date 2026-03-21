#### Concepto
**Ofuscación mediante Hash (Reconocimiento de Algoritmos):** Uso de funciones de resumen (hashing) para generar rutas de archivos dinámicas basadas en variables de entorno (`whoami`).
#### Comandos clave
- `md5sum`: Genera un hash MD5 de la entrada.
- `cut`: Filtra columnas de texto basadas en delimitadores.
#### Resolución
Analicé el script `/usr/bin/cronjob_bandit23.sh` y descubrí que la contraseña de `bandit23` se copiaba a un archivo en `/tmp/` cuyo nombre era el resultado de un hash MD5 de la frase `"I am user bandit23"`. Repliqué manualmente el comando de generación de hash en la terminal para obtener el nombre del archivo y así poder leerlo con `cat`.
#### Aprendizaje
Aprendí que la seguridad por oscuridad (esconder algo bajo un nombre raro) es inútil si el atacante conoce el algoritmo que genera ese nombre. También practiqué el uso de _pipes_ para encadenar lógica de Bash.
#### **`echo I am user bandit23`**
- **Qué hace:** Simplemente imprime esa cadena de texto.
   - **Ojo:** Es la "semilla" del hash. Si le errás a un espacio o una mayúscula, el resultado cambia completamente.
#### **`| md5sum`**
- **MD5 (Message Digest Algorithm 5):** Es una función criptográfica que genera una "huella digital" de 128 bits (32 caracteres hexadecimales) de cualquier dato que reciba.
- **Uso:** En seguridad se usa para verificar la integridad de archivos (que no hayan sido modificados) o, como en este caso, para **ofuscar** nombres de archivos.
- **Dato:** MD5 ya no es seguro para contraseñas reales porque es vulnerable a colisiones, pero para "esconder" archivos temporales en Bandit sigue siendo un clásico.
#### **`| cut -d ' ' -f 1`**
- **`cut`:** Corta pedazos de texto.
- **`-d ' '`:** El delimitador es un **espacio**. (El comando `md5sum` suele devolver el hash seguido de un espacio y un guion).
- **`-f 1`:** Selecciona el primer campo (**f**ield). Esto limpia el hash y te deja solo los 32 caracteres.
#### Pass 23
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
