#### Concepto
Filtrado de texto en archivos masivos mediante patrones específicos.
#### Comandos clave
`grep -oP 'millionth\s+\K\S+' data.txt`
#### Resolución
Ese comando clave exacto devuelve la pass ya que busca el string siguiente a millionth (como dice la consigna en la web). También podía hacerse más simple con `grep "millionth" data.txt`, lo cual devuelve toda la línea.
#### Aprendizaje
##### -o (--only-matching)
Le dice a grep: "No me muestres toda la línea, mostrame **únicamente** la parte que coincide con mi búsqueda".
##### -P (--perl-regexp)
Activa el motor de Perl. Es lo que te permite usar "superpoderes" como `\s` o `\K`, que el grep normal no entiende.
##### millionth\s+\K\S+
- `millionth`: Busca la palabra literal.
- `\s+`: Busca uno o más espacios en blanco.
- **`\K`**: Es el "operador de olvido". Le dice a grep: "Todo lo que encontraste a la izquierda de este punto, **no lo imprimas**". (Por eso no sale la palabra 'millionth' en el resultado).
- `\S+`: Busca uno o más caracteres que **no** sean espacios (la contraseña).
#### Pass 8
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc