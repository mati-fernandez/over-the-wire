#### Concepto
**Exfiltración de Datos vía Git:** El control de versiones (`git`) es una herramienta para desarrolladores, pero en seguridad es una fuente crítica de información. Si un repositorio tiene permisos de lectura, un atacante puede **clonar** el proyecto completo a su máquina local para analizar el código y el historial en busca de credenciales olvidadas.
#### Comandos clave
- **`git clone [URL]`**: Copia un repositorio remoto (incluyendo todo su historial y archivos) a una carpeta local.
- **`ls -la`**: Permite ver archivos ocultos (como la carpeta `.git`) dentro del repositorio clonado.
#### **Anatomía del Comando (La URL)**
La estructura utilizada fue: `ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo`
- **`ssh://`**: Protocolo de transferencia seguro.
- **`bandit27-git`**: Usuario del repositorio (usa la pass de `bandit27`).
- **`bandit.labs.overthewire.org:2220`**: Servidor y puerto del juego.
- **`/home/bandit27-git/repo`**: Ruta física del repositorio **dentro** del servidor de OverTheWire.
#### Resolución
- **Clonación:** Se corrió el comando de git clone. Al pedir la contraseña, se ingresó la del nivel 27.
```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```
- **Inspección:** Se entró a la carpeta creada automáticamente (`cd repo`) y se listaron los archivos.
- **Extracción:** Se leyó el archivo de texto presente (ej. `README`) que contenía la contraseña del siguiente nivel.
#### Aprendizaje
- **Seguridad en Git:** Nunca se deben subir archivos con contraseñas al control de versiones. Aunque se borren después, quedan guardados para siempre en los "commits" anteriores.
- **Local vs Remoto:** El comando `git clone` no solo baja archivos, sino que establece un puente entre tu carpeta local y la ruta absoluta del servidor.
#### Pass 28
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
