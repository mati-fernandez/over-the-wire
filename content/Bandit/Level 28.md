#### Concepto
**Persistencia en el Historial de Git:** Eliminar información sensible en el "presente" (el último commit) no la elimina de la base de datos de Git. Si un archivo fue subido con una contraseña y luego editado para borrarla, la versión original sigue existiendo en los objetos de Git.
#### Comandos clave
- **`git log`**: Muestra la lista cronológica de cambios (commits).
- **`git log -p [archivo]`**: Muestra el historial de un archivo específico detallando qué líneas se borraron (`-`) y cuáles se agregaron (`+`).
- **`git show [commit_id]`**: Permite ver el contenido exacto de un cambio específico en el pasado.
#### Resolución
- **Clonación:** Se descargó el repositorio desde Git Bash.
- **Identificación:** El `README.md` actual tenía la contraseña censurada con `XXXXX`.
- **Investigación:** Se ejecutó `git log -p` para ver qué había antes.
- **Extracción:** Se localizó un commit donde el desarrollador reemplazó la contraseña real por las `X`. La línea marcada en rojo (`-`) contenía la clave válida.
#### Aprendizaje
El historial de Git es inmutable por defecto. Borrar una contraseña en el último 'commit' no la elimina de la base de datos del repositorio. Un atacante siempre puede usar `git log -p` para ver los 'diffs' (diferencias) y recuperar información sensible que fue sobrescrita. La única forma segura de corregir esto en el mundo real es invalidar la contraseña y cambiarla por una nueva (Secret Rotation) o reescribir el historial con herramientas externas (no es buena práctica, sobre todo si se trabaja en equipo).
#### Pass 29
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
