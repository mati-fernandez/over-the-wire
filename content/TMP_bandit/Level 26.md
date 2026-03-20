#### Concepto
**Shell Breakout (Vim Escape):** El usuario `bandit26` tiene como shell `/usr/bin/showtext`, que cierra la sesión al terminar. Para ejecutar comandos complejos (como el binario `bandit27-do`), es necesario forzar al sistema a que nos asigne una shell real (`/bin/bash`) "secuestrando" el proceso de Vim.
#### Comandos clave
- **:set shell=/bin/bash:** Define qué programa debe ejecutar Vim cuando se le pide una shell.
- **:shell:** Comando de Vim para suspender el editor y darnos una terminal interactiva.
- **./bandit27-do [comando]:** Binario SUID que permite ejecutar acciones como el siguiente usuario (`bandit27`).
#### Resolución
- **Punto de entrada:** Se repitió el truco de la ventana pequeña para entrar a `vi`.
- **Configuración de entorno:** Por defecto, la shell de Vim seguía siendo el script restrictivo. Se cambió manualmente con `:set shell=/bin/bash`.
- **Escape:** Se ejecutó `:shell`, lo que finalmente entregó un prompt estable: `bandit26@bandit:~$`.
- **Finalización:** Con la shell real, se ejecutó `./bandit27-do cat /etc/bandit_pass/bandit27` para obtener la siguiente contraseña.
#### Aprendizaje
El "Escape" consiste en cambiar el flujo de ejecución. Pasamos de un script que **lee y cierra** a un editor que **abre y mantiene** una sub-shell. Es la base de la post-explotación en entornos restringidos.
#### Pass 27
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
