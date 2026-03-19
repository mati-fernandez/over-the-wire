#### Concepto
Comunicación con **Servicios de Red** locales. Uso de puertos TCP para intercambio de información.
#### Comandos clave
- `nc` (Netcat): Establece conexiones TCP/UDP arbitrarias.
- `localhost`: Dirección de loopback (tu propia máquina).
#### Resolución
Enviar el string al puerto 3000:
`echo "MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS" | nc localhost 30000`
#### Aprendizaje
Aprendí que no toda la información en un servidor está guardada en archivos de texto (`cat`). Muchos secretos son gestionados por **servicios activos** que escuchan en **puertos TCP/UDP**. Entendí el concepto de `localhost:30000` como una dirección interna y cómo herramientas como `nc` (Netcat) actúan como un "teléfono" para enviar datos a un proceso específico y recibir una respuesta automática del sistema.
#### Pass 15
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo