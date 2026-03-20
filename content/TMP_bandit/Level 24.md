#### Concepto
**Brute-Force Attack:** Automatización de pruebas exhaustivas sobre un espacio de posibilidades (0000-9999) para explotar una debilidad en la autenticación que no tiene límites de intentos (rate limiting).
#### Comandos clave
- **`{0000..9999}`**: Expansión de llaves en Bash para generar secuencias con ceros a la izquierda.
- **`nc localhost [puerto]`**: Establece una conexión TCP para enviar y recibir datos.
- **`grep -v "cadena"`**: Filtra la salida para ocultar el ruido y ver solo el resultado exitoso.
#### Resolución
Para no ver 9,999 mensajes de "Wrong", filtrá la respuesta con `grep`. Solo queremos ver cuando el servidor diga algo diferente (como "Correct" o la contraseña nueva):
```bash
for i in {0000..9999}; do echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"; done | nc localhost 30002 | grep -v "Wrong"
```
**`grep -v "Wrong"`**: El `-v` significa "invertir búsqueda". Le dice a la terminal: "Mostrame todo **MENOS** lo que diga 'Wrong'".
#### Aprendizaje
Aprendí la importancia del **Rate Limiting**. Si este servidor hubiera bloqueado mi IP tras 3 intentos fallidos, este ataque habría sido imposible. También perfeccioné el encadenamiento de comandos para procesar grandes volúmenes de datos.
#### Pass 25
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
