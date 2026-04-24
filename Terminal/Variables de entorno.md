Las variables de entorno son esenciales al trabajar con cualquier sistema operativo, desde Linux hasta Windows o Mac. Representan valores globales que almacenan información clave a la que puedes acceder durante distintos procesos y contextos. Saber gestionarlas te permitirá tener control sobre la configuración de tu sistema operativo y optimizar tu flujo de trabajo.

# ¿Qué son exactamente las variables de entorno?

Una variable de entorno es un tipo especial de variable que guarda información utilizada por el sistema y diversas aplicaciones. Estas variables se invocan en la _shell_ utilizando el símbolo de dólar ($) seguido por el nombre de la variable. Por ejemplo, la variable `SHELL` muestra la dirección del intérprete que utilizamos, como `/bin/bash`.

Variables importantes que debes conocer

- **PWD** (_Print Working Directory_): muestra la ruta actual del directorio en que te encuentras.
- **PATH**: indica una lista de rutas donde el sistema buscará los ejecutables o comandos.
- **LANGUAGE**: proporciona información sobre el lenguaje y codificación utilizados.

# ¿Cómo puedes crear y utilizar tus propias variables de entorno?

Crear variables de entorno es bastante sencillo. Puedes hacerlo directamente en la terminal: escribes el nombre de la variable seguido de su valor. Por ejemplo:

`mybar="saludo" echo $mybar  # imprime saludo`

Sin embargo, estas variables temporales solo viven durante la sesión actual de la terminal.

# ¿Cómo hacer permanentes tus variables?

Para mantener una variable activa en múltiples sesiones, es necesario hacer uso del comando `export`. Dicho comando permite hacer global la variable y que otros programas, como scripts de terceros, tengan acceso a ella:

`export mybar="saludo"`

Si deseas hacer que esta variable persista al cerrar y abrir tus sesiones, debes añadirla en tu archivo de configuración de _shell_, por ejemplo, en Bash sería `.bashrc`:

`echo 'export mybar="saludo"' >> ~/.bashrc`

Es fundamental especificar correctamente esta operación, encapsulando la variable y su valor entre comillas.

Comandos prácticos para gestionar variables de entorno

- Utiliza el comando `env | less` para ver todas las variables existentes en tu sistema de forma ordenada.
- Utiliza `cat ~/.bashrc` para confirmar que la variable se añadió correctamente.

# ¿Por qué son importantes las variables de entorno?

Las variables de entorno son cruciales porque definen configuraciones globales esenciales para diferentes procesos. Por ejemplo, permiten establecer directorios de búsqueda, configuraciones regionales y rutas de ejecución para programas específicos.

Te invitamos a explorar con el comando `env` todas las variables existentes en tu sistema operativo. ¿Cuál ha sido la variable que más te ha interesado o sorprendido? Cuéntanos tu experiencia en los comentarios y comparte tus descubrimientos con la comunidad.