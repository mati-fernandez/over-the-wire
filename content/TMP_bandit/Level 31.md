#### Concepto
**Git Push e Ignored Files:** A veces el reto no es extraer información, sino interactuar con el servidor remoto. Los archivos `.gitignore` se usan para evitar que archivos sensibles o temporales suban al repo, pero en seguridad, esto puede ser una trampa para que el auditor no "vea" o no pueda subir sus herramientas.
#### Comandos clave
- **`git add -f [archivo]`**: El flag `-f` (force) obliga a Git a trackear un archivo aunque esté en la lista negra del `.gitignore`.
- `rm .gitignore`: La otra forma es simplemente borrar ese archivo.
- **`git push`**: Sube tus cambios locales al servidor remoto.
#### Resolución
- **Clonación:** Se clonó el repo del nivel 31.
- **Tarea:** El `README.md` pedía crear un archivo `key.txt` con el contenido `May I come in?`.
- **El Obstáculo:** Al intentar agregarlo, Git lo rechazaba por el `.gitignore`.
- **Bypass:** Se forzó la carga con `git add -f key.txt`.
- **Ejecución:** Se hizo el commit y se subió: `git commit -m "Submit key"` `git push`
- **Extracción:** Al procesar el push, el servidor de OverTheWire ejecutó un script automático que leyó nuestro archivo y nos devolvió la contraseña por la terminal.
#### Aprendizaje
El archivo `.gitignore` no es una medida de seguridad real, es solo una conveniencia para el desarrollador. Como atacante o auditor, siempre hay que revisar qué archivos están siendo ignorados, ya que ahí suelen esconderse archivos de configuración o claves que el desarrollador no quiere que 'viajen' por el repositorio.
#### Pass 32
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
