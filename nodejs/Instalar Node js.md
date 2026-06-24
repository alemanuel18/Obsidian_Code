Trabajar con Node en distintos proyectos exige **cambiar de versión sin dolor**. Aquí aprenderás a diferenciar **LTS**, **actual** y **seguridad**, y a usar **NVM** para instalar, listar y alternar versiones como la 23, la 22.14 LTS o una específica (22.14.1). Todo desde la terminal, de forma segura y práctica.

## ¿Por qué necesitas múltiples versiones de Node?

Cambiar de versión es clave cuando reactivas proyectos “si funciona no lo toques” que dependen de una versión concreta. También cuando quieres probar **características recientes** de la rama **actual** o mantener **actualizaciones de seguridad** en proyectos que ya no evolucionan.

## ¿Qué significan LTS, actual y seguridad en Node?

- **LTS**: versión con _long term support_. Soporte extendido y estabilidad para producción.
- **Actual**: la más reciente en la línea principal, con novedades y cambios activos.
- **Seguridad**: rama que recibe solo parches críticos para proyectos que no se actualizan.

## ¿Qué versiones se mencionan como referencia?

- **Actual**: 23 (ejemplo concreto 23.8).
- **LTS**: 22.14.
- **Anteriores**: 20 y 18, LTS en su momento.

## ¿Cómo instalar y configurar NVM para gestionar Node?

El manejador recomendado es **NVM** (_Node Version Manager_). Permite **instalar varias versiones**, **moverte** entre ellas y **definir un alias default**. Se instala desde la terminal con un script vía `curl` y un pequeño ajuste de configuración.

## ¿Cómo se instala NVM desde la terminal?

- Copia la instrucción de instalación con `curl` y ejecútala en tu terminal.

`# instalación de NVM con curl curl <instrucción_proporcionada>`

- Agrega la instrucción de configuración que define el path de NVM en tu archivo de la terminal.
- Refresca la configuración con `source` según tu _shell_.

`# refrescar configuración de la terminal # si usas ZSH source ~/.zshrc # si usas bash source ~/.bashrc`

- Verifica NVM:

`nvm -d`

Notas de entorno: en Windows se sugiere _Windows Subsystem Linux_ (WSL) para correr comandos de estilo _UNIX_/_Linux_. En _macOS_ y GNU/Linux ya cuentas con estos comandos en la terminal. Si usas ZSH, puedes personalizarlo a tu gusto.

## ¿Cómo instalar, listar y cambiar versiones con NVM?

Con NVM puedes preparar tu entorno para producción con **LTS**, probar la **actual** o fijar una **versión exacta** para un proyecto.

## ¿Cómo listar e instalar versiones de Node?

- Listar lo instalado.

`nvm ls`

- Instalar la versión mayor 23. NVM detecta y descarga la 23.8.

`nvm install 23`

- Ver que se definió como **default** automáticamente.

`nvm ls`

- Instalar la **LTS** 22.

`nvm install 22`

- Instalar una versión específica (ejemplo: 22.14.1).

`nvm install 22.14.1`

## ¿Cómo cambiar y validar la versión activa?

- Cambiar entre versiones según el proyecto.

`nvm use 22 
`nvm use 23 
`nvm use default`

- Validar la versión de Node en uso.

`node -b`

## Buenas prácticas destacadas:

- Instala la **más reciente** como principal y muévete gradualmente según el caso.
- En producción usa **LTS** para estabilidad y soporte predecible.
- Para proyectos antiguos, primero **cámbiate** a la versión que el proyecto requiere.