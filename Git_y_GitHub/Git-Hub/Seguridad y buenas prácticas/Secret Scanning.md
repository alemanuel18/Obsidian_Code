Subir por accidente una API key o una cadena de conexión al repositorio es uno de los errores más comunes en desarrollo. GitHub ofrece **Secret Scanning** y **Code Scanning** como red de seguridad para detectar esas filtraciones antes de que alguien las explote, y aquí verás cómo activarlas, probarlas y entender sus límites reales.

## ¿Por qué necesitas escanear secretos en tu repositorio?

Un archivo _gitignore_ bien configurado evita que subas archivos sensibles, pero no protege contra el descuido humano. Puedes escribir una llave directamente dentro del código fuente y, sin darte cuenta, hacer _push_ de información que compromete cuentas de terceros.

Entre los datos delicados que suelen filtrarse están:

- Llaves de acceso a APIs externas como Stripe.
- Cadenas de conexión a bases de datos.
- Tokens de autenticación o credenciales de servicios cloud.

> **¿Qué es un secreto en GitHub?** Es cualquier credencial, token o llave que da acceso a un servicio. Si queda expuesto en un commit, cualquiera con acceso al repositorio puede usarlo.

## ¿Cómo activar Code Scanning y Secret Scanning en GitHub?

Estas funciones solo aparecen disponibles cuando tu repositorio es **público**, así que el primer paso es revisar la visibilidad en la _danger zone_ de los settings .

Una vez público, entra a **Settings > Code security and analysis** y configura lo siguiente:

1. Localiza la sección _Code scanning_ y selecciona **CodeQL analysis**.
2. Deja la configuración por defecto, donde GitHub detecta automáticamente el lenguaje del proyecto (en este ejemplo, C#).
3. Habilita CodeQL y confirma los criterios de búsqueda.
4. Baja a _Secret scanning_: viene activado por defecto, con un botón para deshabilitar.

## ¿Qué hace CodeQL exactamente?

CodeQL analiza el código fuente buscando patrones de vulnerabilidad. Trabaja en segundo plano cada vez que haces _push_, sin que tengas que ejecutarlo manualmente.

## ¿Cómo reacciona GitHub ante una API key filtrada?

Para probar la herramienta, basta con escribir en _program.cs_ una línea como `string stripeApiKey` con un valor entre comillas simulando una credencial real . Después aplicas la secuencia habitual:

- `git status` para confirmar el cambio.
- `git add` y `git commit` con un mensaje descriptivo.
- `git push` para enviarlo al repositorio.

Al regresar al repositorio, aparece un círculo amarillo de **pending** mientras GitHub evalúa los cambios. Tras refrescar la página, la pestaña _Security_ muestra un **1** en alertas. Y aquí viene lo interesante: dentro encuentras tres categorías de alertas, **Dependabot**, **Code Scanning** y **Secret Scanning**, y en esta última está la notificación de la llave detectada.

> **¿Qué hago si GitHub detecta un secreto filtrado?** Rota la credencial en el servicio de origen, modifica tu código para usar variables de entorno y recuerda que borrar la línea no la elimina del historial de commits.

## ¿Cuáles son los pasos para mitigar la filtración?

GitHub recomienda cuatro pasos que aplican a casi cualquier secreto expuesto:

1. Contactar al proveedor (la cuenta de terceros) y rotar las credenciales.
2. Invalidar la llave anterior para que ya no funcione.
3. Modificar el código para mover el secreto a variables de entorno.
4. Confirmar que el flujo nuevo no vuelva a filtrar el dato en futuros commits.

## ¿Por qué Secret Scanning no detecta todos los secretos?

Aquí está el matiz que muchos pasan por alto. Cuando escribes algo evidente como `stripeApiKey`, GitHub lo identifica rápido por el patrón conocido. Pero si nombras la variable `string testingConnection` y pegas una cadena de conexión SQL real, la herramienta no genera ninguna alerta .

Después de esperar cuatro minutos para confirmar que el escaneo terminó, la única alerta visible sigue siendo la de Stripe. La cadena de conexión a SQL pasó desapercibida porque el nombre de la variable no coincidía con patrones reconocibles como _sql connection_ o _sql key_.

La lección es clara: **Secret Scanning ayuda, pero no es infalible**. Detecta patrones bien documentados de proveedores conocidos, no cualquier credencial disfrazada con un nombre genérico.

## ¿Cuál es la mejor estrategia para proteger tus credenciales?

La frase que resume todo es simple: siempre será más fácil **prevenir que lamentar**. Las herramientas de escaneo son una segunda línea de defensa, no la primera.

Tu flujo ideal debe verse así:

- Guarda credenciales en archivos `.env` o `appsettings.json` según tu lenguaje.
- Añade esos archivos al **gitignore** para excluirlos del control de versiones.
- Usa variables de entorno en tu código en lugar de valores hardcodeados.
- Mantén Code Scanning y Secret Scanning activos como respaldo.

Si adoptas estas prácticas desde el inicio, las alertas de seguridad de GitHub serán algo que casi nunca verás. Y eso es exactamente lo que quieres, porque rotar llaves o cadenas de conexión en producción es un proceso complicado: tu producto rara vez es el único consumidor de esas credenciales, y cada cambio puede romper integraciones con otros servicios.