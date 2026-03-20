#### Concepto
**Lectura de archivos vía Editor (Vim):** En lugar de intentar obtener una shell funcional, se aprovecha que el paginador `more` permite saltar a un editor (`vi`). Una vez dentro del editor, se pueden usar comandos internos para leer archivos que el usuario tiene permitidos, incluso si la shell interactiva está bloqueada.
#### Comandos clave
- **ssh -i mi_llave_26 bandit26@bandit.labs.overthewire.org -p 2220:** Conexión directa desde máquina local para evitar el bloqueo de `localhost` (tuve que salir de bandit25)
- **stty rows 3:** Obliga al servidor a paginar el texto de bienvenida (redimensioné manualmente la ventana igual, no sé si este comando era necesario pero es buena práctica).
- **v (dentro de more):** Abre el editor `vi`.
- **:r [archivo]:** Lee (read) el contenido de un archivo y lo vuelca en el buffer actual del editor.
#### Resolución
- **Extracción:** Se obtuvo la clave privada `bandit26.sshkey` desde el nivel 25.
- **Bypass de Red:** Se intentó conectar desde `bandit25@localhost`, pero el servidor rechazó la conexión por seguridad ("Connecting from localhost is blocked"). Se optó por conectar desde mi PC usando la llave copiada.
- **Forzado de Paginación:** Se achicó la ventana y se usó `stty rows 3`. Al conectar, el texto de bienvenida se detuvo en `--More--`.
- **Acceso Directo:** Se presionó `v` y, dentro de `vi`, se ejecutó `:r /etc/bandit_pass/bandit26`. Esto permitió ver la contraseña sin haber "escapado" a una shell todavía.
#### Aprendizaje
A veces no es necesario "romper" el sistema para obtener el secreto. Si tienes acceso a un editor de texto con privilegios del usuario objetivo, puedes leer la información sensible (`/etc/bandit_pass/...`) directamente desde el buffer del editor.
#### Por qué te rechazaba Bandit 25?
Los servidores de OverTheWire bloquean conexiones SSH de `localhost` a `localhost` en el puerto `2220` para evitar que los usuarios consuman todos los recursos del sistema creando túneles infinitos. Al hacerlo desde tu **WSL**, el servidor te ve como una conexión externa legítima y te deja pasar.
**Clave del éxito:** No se puede saltar al Level 26 desde la sesión de Bandit 25 debido al bloqueo de _localhost_. Es obligatorio **exfiltrar la llave privada** (copiar su texto), crear el archivo en la máquina local (`chmod 600`) y realizar una conexión limpia desde afuera. Sin este paso, el servidor nos expulsa antes siquiera de que el comando `more` pueda ejecutarse.
#### Pass 26
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
