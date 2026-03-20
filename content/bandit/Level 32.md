#### Concepto
**Shell Escape (Insecure Shell Wrapper):** Algunos entornos restringidos usan "wrappers" (envoltorios) que procesan la entrada del usuario antes de ejecutarla. En este caso, el wrapper convertía todo a mayúsculas, impidiendo ejecutar comandos estándar de Linux (que son casi todos en minúsculas). Sin embargo, las variables de entorno especiales como `$0` no se ven afectadas por la conversión a mayúsculas.
#### Comandos clave
- **`$0`**: En sistemas Unix, esta variable contiene el nombre del programa que se está ejecutando (usualmente la shell actual).
- **`/etc/bandit_pass/bandit33`**: Ubicación estándar de la contraseña.
#### Resolución
- **Análisis:** Al ingresar al nivel 32, cualquier comando como `ls` o `cat` fallaba porque se transformaba en `LS` o `CAT`.
- **Identificación:** Se detectó que el sistema usaba una técnica de "Positional Parameters". En Bash, `$0` invoca al ejecutable que inició la sesión actual.
- **Evasión:** Se ingresó simplemente `$0`. Como el símbolo `$` y el número `0` no tienen representación en mayúsculas, el "filtro" no pudo alterarlos.
- **Escape:** El sistema ejecutó el comando almacenado en `$0`, lo cual abrió una shell convencional (`sh`) libre de las restricciones de mayúsculas.
- **Extracción:** Ya en la shell normal, se ejecutó `cat /etc/bandit_pass/bandit33` para obtener la clave.
#### Aprendizaje
Confiar en filtros de texto simples (como pasar a mayúsculas) para restringir una shell es una vulnerabilidad grave. Siempre existen variables de entorno o caracteres especiales que el filtro no contempla. Como atacante, probar variables internas del sistema como `$0`, `$SHELL` o `env` es el primer paso para romper una jaula (jailbreak).
#### Pass 33
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
