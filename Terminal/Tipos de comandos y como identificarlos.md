# ¿Cómo identificar qué es exactamente cada comando?

Son varias las herramientas que Linux ofrece para identificar el tipo y las características de los comandos que usamos diariamente. Aquí exploraremos algunas que debes conocer:

# ¿Qué es un alias en Linux y cómo reconocerlo?

Un alias funciona como un apodo en el sistema operativo Linux, permite ejecutar comandos con ciertas opciones de manera más fácil o vistosa. Por ejemplo, el comando `ls` que generalmente usamos para listar directorios, en realidad es un alias de `ls --color=auto` para mostrar resultados con colores. Para verificar si un comando es un alias, puedes ejecutar:

`type ls`

Esta instrucción genera una salida que indica si el comando es un alias y cuál es su composición específica.

# ¿Dónde se ubican los comandos originales?

Si deseas encontrar la ruta precisa del comando que estás usando, la instrucción `which` será fundamental:

`which ls`

Este comando te mostrará la ubicación exacta del archivo ejecutable original, distinto al alias que podrías estar usando.

Además, para obtener más ubicaciones relacionadas con un comando específico, puedes utilizar `whereis`. Este comando te dará un panorama más amplio:

`whereis ls`

Generalmente verás rutas como `/usr/bin/ls`, indicando dónde residen la mayoría de los comandos importantes y esenciales del sistema operativo.

# ¿Cómo obtener información rápida sobre la función de un comando?

Para obtener rápidamente información sobre qué función cumple cualquier comando, utiliza `whatis`. Este comando te devuelve breve y claramente la tarea principal del comando consultado:

`whatis grep`

La respuesta, en este caso, indica que `grep` es capaz de encontrar líneas según patrones específicos.

# ¿Qué tipos de comandos existen en Linux?

En términos prácticos, los comandos ejecutables dentro de Linux pueden pertenecer a alguna de estas categorías:

- **Binarios compilados:** usualmente creados en lenguajes como C++.
- **Scripts en diversos lenguajes:** incluyendo shell scripts o scripts de Python o JavaScript.
- **Alias:** comandos personalizados que simplifican o embellecen la experiencia visual en la terminal.
- **Utilidades propias del sistema operativo:** herramientas básicas esenciales para la operación general del sistema.

Te recomendamos explorar dentro del directorio `/usr/bin`, donde se ubica gran parte de los comandos estándares del sistema. Es importante que recuerdes que algunos comandos adicionales pueden provenir de paquetes gestionados mediante `npm` (JavaScript), paquetes de Python u otros lenguajes que generen binarios globales.