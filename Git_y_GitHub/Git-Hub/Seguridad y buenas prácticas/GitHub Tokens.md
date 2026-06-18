Cuando trabajas con repositorios privados en GitHub, tarde o temprano necesitarás otorgar acceso temporal a otra persona o a una aplicación sin convertirla en colaborador permanente. Los **GitHub Tokens** o _Personal Access Tokens_ resuelven exactamente este problema: funcionan como llaves temporales con privilegios controlados que tú defines, garantizando que quien las reciba solo pueda hacer lo que tú autorices y únicamente donde tú lo permitas.

## ¿Cómo se crea un repositorio privado para usar con tokens?

El primer paso es contar con un repositorio privado. Desde GitHub, selecciona el signo de más y elige la opción de nuevo repositorio . Asigna un nombre, marca la opción **privado** y agrega un _README_ junto con un archivo _.gitignore_ según el lenguaje que prefieras. Una vez creado, tú como propietario puedes clonarlo fácilmente con HTTPS o SSH, pero cualquier otra persona necesitará credenciales específicas para acceder.

Para generar esas credenciales, ve a tu foto de perfil en la esquina superior derecha, selecciona _Settings_ y busca la última opción en el menú izquierdo: **Developer settings** . Aquí encontrarás tres secciones principales: aplicaciones con acceso autorizado, aplicaciones validadas mediante autenticaciones y, la más relevante, los tokens.

## ¿Cuál es la diferencia entre tokens clásicos y tokens detallados?

GitHub ofrece dos tipos de tokens con características muy distintas.

## ¿Qué permite un token clásico?

Los **tokens clásicos** te permiten asignar permisos por categoría general . Al generar uno, defines:

- Un **nombre identificativo**, como "Token Admin 02", idealmente con el nombre de la persona o aplicación que lo usará.
- Una **fecha de expiración**, que puede ser desde siete días hasta "sin expiración" (aunque esta última opción no es segura).
- **Privilegios** como acceso a repositorios, escritura de paquetes (_NuGet_, _NPM_, _PIP_), _Gists_ y notificaciones.

Una vez generado, GitHub muestra el código del token **una sola vez** . Si no lo copias antes de salir de la página, tendrás que eliminar ese token y crear uno nuevo. No hay forma de recuperarlo después.

## ¿Por qué elegir un token detallado o _fine-grained_?

Los **tokens detallados** representan una evolución significativa en seguridad . Sus diferencias principales son:

- La expiración máxima es de **noventa días** y no existe la opción de "sin expiración".
- Puedes seleccionar el **propietario de los recursos**: tu cuenta personal o cualquier organización que administres.
- El alcance se puede limitar a **repositorios específicos**, no solo por tipo (público o privado) . Por ejemplo, puedes restringir el token para que solo acceda a un repositorio en particular.
- Los permisos son extremadamente granulares: GitHub ofrece decenas de opciones para definir exactamente qué puede leer y escribir el token .

Al finalizar la configuración, un _overview_ te muestra un resumen con la cantidad de permisos habilitados y la fecha de expiración . El token generado comienza con el prefijo `github_pat_` y es considerablemente más largo que un token clásico.

## ¿Cómo se usa un token para clonar un repositorio privado?

El flujo en la terminal es idéntico al que ya conoces con `git clone`, pero con un paso adicional de autenticación . Al ejecutar el comando con la URL HTTPS del repositorio, la terminal solicita tu **nombre de usuario** de GitHub y luego un _password_.

Aquí está el detalle clave: **no puedes usar la contraseña de tu cuenta** si tienes habilitada la verificación en dos pasos . En su lugar, debes pegar el _Personal Access Token_ que generaste. Linux, por ejemplo, no muestra el texto al pegarlo, pero el proceso funciona correctamente. Después de autenticarte, la descarga del repositorio ocurre de manera normal.

Este mismo proceso aplica tanto si estás en un equipo ajeno sin tus credenciales como en tu propia máquina que aún no tiene configuración de GitHub.

Los usos prácticos de los tokens van mucho más allá de clonar repositorios. Sirven para **automatizar tareas con GitHub Actions**, crear _workflows_ personalizados o ejecutar _scripts_ que realicen _commits_ automáticos en intervalos regulares . Lo fundamental es mantener siempre la seguridad como prioridad: que los tokens expiren en un plazo razonable, que tengan acceso exclusivamente a lo necesario y que cumplan únicamente la función para la que fueron creados.