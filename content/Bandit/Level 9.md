#### Concepto
Extracción de datos legibles dentro de un **archivo binario** (no de texto plano). El objetivo es filtrar el "ruido" o código de máquina para encontrar cadenas de caracteres que un humano pueda leer, utilizando un patrón visual (`=`) como guía.
#### Comandos clave
- `strings`: Filtra un archivo y devuelve solo las secuencias de caracteres imprimibles.
- `grep`: Busca patrones específicos dentro de la salida de otros comandos.
- `|` (Pipe): Conecta la salida de un comando con la entrada del siguiente.
#### Resolución
`strings data.txt | grep "=="`
_Se observa que la contraseña está precedida por varios signos de igual._
#### Aprendizaje
Aprendí que los archivos binarios no son "ilegibles" por completo; contienen metadatos y strings que pueden revelar información sensible. También comprendí el uso de `strings` para limpiar basura visual antes de aplicar filtros de búsqueda.
##### Cómo hacer el comando "Nivel Pro"
Para que `grep` agarre **todos** los iguales sin importar cuántos sean y que además te limpie la salida, podés usar **Expresiones Regulares (Regex)**.
1. Agarrar todos los iguales (sin dejar uno suelto)
Usamos el cuantificador `+`, que significa "uno o más de lo anterior". Como el `+` es un carácter especial, usamos `grep -E` (Extended Regex):

```bash
strings data.txt | grep -E "=+"
```
Esto le dice a Linux: "Buscame cualquier secuencia donde el símbolo `=` aparezca una o infinitas veces seguidas". Así no te queda ninguno en blanco.
##### 2. El modo "Ninja": Limpiar los iguales de la respuesta
Si querés que la terminal te devuelva **solo** la contraseña y borre los iguales automáticamente, podés usar `grep -o` (only matching) con una expresión un poco más avanzada:
```bash
strings data.txt | grep -oE "[a-zA-Z0-9]{10,}"
```
- **`[a-zA-Z0-9]`**: Busca solo letras y números (ignora los `=`).
- **`{10,}`**: Le dice que solo te muestre ráfagas de texto que tengan **10 o más caracteres** de largo.
Como la contraseña es larga y los iguales son símbolos, este comando "limpia" los `=` y te escupe la clave pura.
#### Pass 10
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey