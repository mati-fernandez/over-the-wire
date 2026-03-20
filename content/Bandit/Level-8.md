#### Concepto
Filtrado de líneas únicas mediante el ordenamiento previo de datos.
#### Comandos clave
`sort data.txt | uniq -u`
#### Resolución
El archivo `data.txt` tiene miles de líneas. Como `uniq` solo compara líneas adyacentes, primero usamos `sort` para agrupar todas las líneas idénticas. Luego, usamos `uniq -u` para descartar todas las que tengan duplicados, dejando únicamente la contraseña que aparece una sola vez.
#### Aprendizaje
- **`sort`**: Indispensable antes de usar `uniq`.
- **`uniq -u`**: Devuelve solo lo que no tiene copias (Unique).
- **`uniq -c`**: (Tip extra) Cuenta cuántas veces aparece cada línea.
#### Pass 9
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM