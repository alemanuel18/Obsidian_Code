La terminal es una poderosa herramienta que no solo permite ejecutar comandos locales, sino también interactuar activamente con recursos en la red e Internet. Mediante comandos sencillos, puedes obtener información precisa sobre tus conexiones, realizar peticiones, descargar recursos y verificar el estado de servidores remotos desde la comodidad de tu línea de comandos.

# ¿Cómo consultar direcciones IP e interfaces de red desde la terminal?

El comando **IP** es especialmente práctico para listar interfaces, direcciones asignadas y otras configuraciones relacionadas con la red. Su ejecución básica es:

`ip a`

Esta opción muestra dos interfaces típicas:

- La interfaz local o loopback con IP predeterminada `127.0.0.1`.
- La interfaz conectada a tu red local o externa, indicando claramente tu dirección IPv4 local actual.

# ¿Qué revela nuestra tabla de ruteo utilizando la terminal?

Leer la tabla de ruteo es sencillo con el comando:

`ip r`

A partir de la respuesta, observarás claramente cuáles dispositivos están interconectados, rutas predeterminadas establecidas y sus respectivas IP. Esta herramienta es clave para verificar tu configuración de red, especialmente en entornos con múltiples conexiones.

¿Cómo verificar la disponibilidad y respuesta de recursos web con el comando ping?

**Ping** envía paquetes a un recurso web determinado, como por ejemplo:

`ping www.google.com`

Al ejecutarlo, descubrirás en tiempo real si un sitio responde adecuadamente o si existe alguna pérdida de paquete. Esto indica inmediatamente la disponibilidad y estabilidad del recurso seleccionado.

Presionar `Control + C` interrumpe el proceso y muestra un resumen claro de su funcionamiento.

# ¿Qué puedo hacer con el comando curl en peticiones HTTP?

**Curl** es un potente mini cliente HTTP con el que puedes realizar diversas peticiones, incluyendo GET y POST, entre otras. Aplicado a un sitio web, descarga directamente su contenido HTML:

`curl www.google.com`

Además, puedes guardar el contenido directamente a un archivo:

`curl www.google.com > index.html`

Esto abre oportunidades prácticas para automatizar procesos web desde la terminal.

# ¿Cómo descargar archivos desde Internet utilizando wget?

El comando **wget** facilita descargar archivos directamente de Internet a través de la terminal, solo es necesario proporcionar la URL del recurso:

`wget <URL_RECURSO>`

Una vez que finaliza la descarga, el archivo queda fácilmente accesible en tu directorio de trabajo actual.

# ¿Cuál es la utilidad de herramientas avanzadas como nmap y traceroute?

Aunque estos comandos son algo más específicos, su utilidad es bastante destacable:

- **nmap**: escanea puertos de la computadora, determinando servicios expuestos o funcionalidades activas.
- **traceroute**: rastrea el recorrido exacto de paquetes enviados hacia un destino, evidenciando qué servidores atraviesa en camino al recurso solicitado.