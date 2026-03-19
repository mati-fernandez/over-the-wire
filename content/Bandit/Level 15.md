#### Concepto
**Cifrado de transporte (SSL/TLS)**. Uso de túneles seguros para envío de datos sensibles.
#### Comandos clave
- `openssl s_client`: Cliente genérico para conectar a servicios con SSL/TLS.
- `-connect`: Flag para especificar host y puerto.
- `-ign_eof`: Previene el cierre prematuro de la conexión tras enviar datos (no la usé).
#### Resolución
`openssl s_client -connect localhost:30001`
Establecí una conexión cifrada al puerto `30001` de `localhost` usando el cliente de OpenSSL. Una vez establecido el apretón de manos (handshake), envié la contraseña actual y el servicio respondió con la del siguiente nivel.
#### Aprendizaje
Aprendí que existen puertos que no aceptan conexiones de texto plano por seguridad. Entendí que SSL/TLS no es solo para páginas web (HTTPS), sino que puede envolver cualquier comunicación por puerto para proteger los datos de posibles "sniffers" (chismosos) en la red.
#### Diferencia con el nivel anterior
- Mientras que `nc` solo abre un tubo de datos básico, `s_client` primero hace el "apretón de manos" (handshake): intercambia certificados, negocia el algoritmo de cifrado y establece un túnel seguro.
- Solo después de que ese túnel es irrompible, te deja escribir.
#### Pass 16
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx