#### Concepto
Cifrado por sustitución (ROT13).
#### Comandos clave
`tr` (Translate).
#### Resolución
 `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
Para resolver este nivel, utilicé el comando `tr` (translate) para aplicar un descifrado **ROT13**. Dado que `tr` no entiende de rotaciones matemáticas, le proporcioné dos conjuntos de caracteres para realizar un mapeo directo:
1. **Conjunto de búsqueda (`'A-Za-z'`):** Representa el alfabeto estándar completo.
2. **Conjunto de reemplazo (`'N-ZA-Mn-za-m'`):** Define el nuevo orden. Al escribir `N-ZA-M`, le indico a la herramienta que el rango debe "dar la vuelta": comienza en **N**, llega hasta la **Z** y continúa inmediatamente desde la **A** hasta la **M**.
De esta forma, cada letra del archivo `data.txt` fue sustituida por su par correspondiente 13 posiciones adelante, revelando la contraseña en texto plano.
#### Aprendizaje
Cómo mapear rangos de caracteres para desplazar el alfabeto. Entendí que ROT13 es reversible con el mismo comando.
#### Pass 12
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

