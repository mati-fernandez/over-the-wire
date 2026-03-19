#### Concepto
**Fuga de información en Ramas (Branches):** En proyectos reales, los desarrolladores usan diferentes ramas para organizar el trabajo (ej. `main`, `dev`, `fix`). A veces, la rama principal está "limpia", pero las ramas de desarrollo o experimentales contienen credenciales que olvidaron borrar antes de fusionar o que simplemente quedaron ahí "vivas".
#### Comandos clave
- **`git branch -a`**: Lista todas las ramas, incluyendo las remotas (`remotes/origin/...`) que no descargaste todavía.
- **`git checkout [rama]`**: Cambia el estado de tu carpeta local a la versión de esa rama.
- **`git log --all`**: Muestra el historial de todas las ramas existentes, no solo en la que estás parado.
#### Resolución
- **Clonación:** Se bajó el repo del nivel 29. El `README.md` decía que no había passwords en producción.
- **Detección:** Se ejecutó `git branch -a` y se descubrió una rama remota llamada `dev` (o similar).
- **Inspección:** En lugar de cambiar de rama, se usó un comando más directo para ver todos los commits de todas las ramas y sus hashes: `git log --all --oneline`.
- **Extracción:** El commit en la rama de desarrollo contenía la contraseña que en la rama principal había sido reemplazada por el mensaje de "no passwords". Se logró obtener con `git show e50e6cc` siendo este último el commit hash (id del commit).
#### Aprendizaje
No basta con revisar la rama principal (`main/master`). Al auditar un repositorio, es obligatorio revisar **todas** las ramas y sus historiales. Las ramas de 'dev' o 'test' son minas de oro para encontrar configuraciones de depuración y claves de acceso que nunca deberían haber salido del entorno local del desarrollador.
#### Pass 30
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
