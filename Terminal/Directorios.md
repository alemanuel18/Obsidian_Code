# CD
## ¿Qué es navegar con rutas absolutas?

Una ruta absoluta comienza siempre desde la raíz del sistema operativo, especificada por un slash (/). Por ejemplo, usar el comando `cd /` nos posiciona directamente en el directorio raíz del sistema Linux, que aloja importantes carpetas del sistema tales como:

- bin
- dev
- lib64
- root
- home

Este método permite acceder directamente a cualquier directorio proporcionando su ruta completa.

## ¿Cómo funcionan las rutas relativas y símbolos especiales?

Mientras que las absolutas requieren especificar toda la ruta desde la raíz, las relativas funcionan desde el lugar actual en que nos encontramos. Uso frecuente de símbolos clave:

- Punto (`.`) para indicar el directorio actual.
- Doble punto (`..`) para subir un nivel de directorio.
- Virgulilla (`~`) para referencia rápida al directorio home del usuario actual.

Esto permite desplazarnos rápidamente usando comandos como `cd ..` para retroceder y `cd ~` para ir al home del usuario rápidamente, independientemente del directorio actual.

# `pushd` y `popd`

Ambos comandos facilitan almacenar temporalmente una ubicación y regresar posteriormente a ella:

- `pushd`: guarda la ubicación actual en una pila.
- `popd`: recupera la última ubicación almacenada y nos desplaza automáticamente a ella.

Este mecanismo es muy útil para navegar cómodamente cuando trabajamos en múltiples directorios simultáneamente.
