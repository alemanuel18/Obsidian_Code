Usar un manejador de paquetes como APT te permite administrar fácilmente la instalación, actualización y eliminación de software directamente desde la terminal. Conocer el uso efectivo de APT es crucial para mantener tu sistema operativo Linux, especialmente en distribuciones basadas en Debian como Ubuntu, actualizado y bien administrado.

# ¿Qué es un manejador de paquetes?

Un manejador de paquetes es un sistema que funciona como una tienda de aplicaciones, permitiéndote administrar software mediante comandos específicos desde la terminal. Varía según el sistema operativo:

- Debian y derivados: APT.
- Red Hat o Fedora: DNF o Yum.
- Arch Linux: Pacman.
- macOS: no tiene uno nativo, pero la comunidad creó Vroom.

En esta ocasión, profundizaremos en APT, propio de Debian y derivados.

# ¿Cómo funciona el comando APT?

APT (_Advanced Package Tool_) gestiona los paquetes y comandos nuevos que necesites instalar en tu sistema. Las funciones principales de APT incluyen:

- Instalar paquetes usando `sudo apt install nombre-paquete`.
- Verificar información sobre paquetes con `apt show nombre-paquete`.
- Actualizar información de paquetes disponibles mediante `sudo apt update`.
- Revisar actualizaciones disponibles con `apt list --upgradeable`.
- Aplicar actualizaciones utilizando `sudo apt upgrade`.

Siempre ejecuta estos comandos como superusuario utilizando `sudo` para garantizar la efectividad y seguridad del proceso.

# ¿Cómo actualizar los paquetes del sistema operativo con APT?

La actualización del sistema operativo implica dos pasos principales claramente distintos:

1. Primero actualizar la base de datos de paquetes disponibles:

`sudo apt update`

2. Después actualizar los paquetes instalados:

`sudo apt upgrade`

Este procedimiento mantiene tu sistema al día con los últimos paquetes disponibles en los repositorios.

# ¿Cómo instalar un nuevo paquete con APT?

La instalación de paquetes nuevos es muy sencilla. Aquí te mostramos cómo instalar _NeoFetch_, un paquete que muestra información del sistema:

`sudo apt install neofetch`

Una vez instalado, ejecuta directamente el nuevo comando desde la terminal:

`neofetch`

# ¿Cómo eliminar paquetes usando APT?

Eliminar paquetes también es fácil y rápido. Puedes hacerlo utilizando:

- Para remover un paquete:

`sudo apt remove nombre-paquete`

- Para eliminar profundamente un paquete y sus archivos de configuración:

`sudo apt purge nombre-paquete`

Esto asegura que tanto el paquete como las dependencias y configuraciones relacionadas se remuevan completamente de tu sistema.

# ¿Por qué es importante familiarizarse con distintos manejadores?

Aunque las funciones básicas como instalar, actualizar o eliminar paquetes son similares en todos los manejadores, los comandos específicos pueden variar notablemente. Por ejemplo, APT utiliza comandos fáciles de entender, mientras que Pacman utiliza flags.

Si te encuentras con manejadores diferentes en otras distribuciones, la mejor estrategia es consultar la documentación respectiva para resolver cualquier duda o diferencia específica en su uso.

Te invito a compartir cualquier pregunta que tengas en los comentarios para poder apoyarte en tus primeros pasos con los manejadores de paquetes.