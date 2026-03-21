#### Concepto
**Git Tags (Etiquetas):** Los tags se usan para marcar puntos específicos en la historia (como versiones `v1.0`). Sin embargo, pueden ser usados para almacenar información sensible en sus metadatos o para señalar commits que no están vinculados a ninguna rama activa, haciéndolos menos visibles a simple vista.
#### Comandos clave
- **`git tag`**: Lista todas las etiquetas del repositorio.
- **`git show [nombre_tag]`**: Muestra los detalles y el contenido asociado a esa etiqueta.
#### Resolución
- **Clonación:** Se clonó el repositorio del nivel 30.
- **Exploración:** `ls -la` y `git log` no mostraron nada útil.
- **Detección:** Se ejecutó `git tag` y se encontró una etiqueta llamada `secret`.
- **Extracción:** Al ejecutar `git show secret`, el sistema devolvió la contraseña del siguiente nivel.
#### Aprendizaje
No todo lo que existe en un repositorio Git está en los archivos o en el historial de las ramas. Los objetos como los **Tags** pueden contener referencias a datos que no aparecen en la rama principal. Un análisis forense de Git debe incluir siempre la revisión de etiquetas.
#### Pass 31
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
