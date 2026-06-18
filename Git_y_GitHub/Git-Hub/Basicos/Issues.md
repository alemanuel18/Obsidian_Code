Los _issues_ en GitHub son la forma más directa de reportar errores, sugerir mejoras o documentar fallos en un repositorio. Si estás aprendiendo control de versiones, dominar esta herramienta te permite colaborar con otros desarrolladores y recibir retroalimentación clara sobre tu código.

Aquí aprenderás a crear un _issue_ desde cero, configurar una plantilla _bug report_ dentro de tu repositorio y entender por qué este flujo mejora la experiencia de quienes quieren contribuir a tu proyecto.

## ¿Qué es un issue en GitHub y para qué sirve?

Un _issue_ es un mecanismo para señalar defectos o mejoras dentro de un repositorio. Puede tratarse de algo tan pequeño como un acento faltante en la documentación o tan complejo como una falla funcional en el comportamiento esperado del código.

La idea central es comunicarle al autor que existe un problema. A partir de ahí, tú decides si solo reportas el detalle o si además contribuyes con la solución.

> **¿Qué es un issue en GitHub?** Es un reporte público dentro de un repositorio que documenta un error, una mejora o una pregunta. Sirve para que cualquier persona avise al autor sobre algo que no funciona como se espera.

## ¿Cómo creo un nuevo issue paso a paso?

Dentro de tu repositorio, entra a la pestaña **Issues** y selecciona el botón de nuevo _issue_. Aparece un formulario con dos campos esenciales: título y descripción.

- En el título escribe algo claro, por ejemplo: _no hay más documentos_.
- En la descripción detalla qué está pasando y cómo reproducirlo.
- En la columna derecha puedes asignar responsables, agregar etiquetas y otros metadatos opcionales.

Una vez enviado, verás el contador subir a uno y el hilo queda abierto para conversación pública.

## ¿Cómo crear una plantilla de issues bug report?

Para facilitarle la vida a quienes reportan errores, GitHub permite crear plantillas. Así, en lugar de una hoja en blanco, tus colaboradores reciben un formulario guiado .

Abre tu terminal en la carpeta del repositorio y ejecuta el comando `code .` para abrir Visual Studio Code. Desde ahí trabajarás directamente sobre los archivos.

## ¿Qué estructura de carpetas necesito?

GitHub espera una convención específica para reconocer las plantillas. Si la estructura no es exacta, no aparecerán al crear un _issue_.

1. Crea una carpeta llamada `.github` (con el punto inicial, esto es obligatorio).
2. Dentro de ella, crea otra carpeta en mayúsculas: `ISSUE_TEMPLATE`.
3. Dentro de esa segunda carpeta, crea un archivo llamado `bug_report.md`.

La extensión `.md` corresponde a _Markdown_, el mismo lenguaje del archivo README. Copia el contenido base desde los recursos de la clase y pégalo dentro del archivo.

> **¿Por qué la carpeta debe llamarse .github?** Porque GitHub busca esa ruta específica para detectar configuraciones especiales como plantillas de _issues_, _pull requests_ o flujos de automatización.

## ¿Cómo subo los cambios al repositorio remoto?

Visual Studio Code marca en verde los archivos y carpetas nuevos, indicando que hay cambios pendientes en el control de versiones. Ve a la sección de control de cambios y verás que `bug_report` aparece listo para registrarse.

- Escribe un mensaje de _commit_, por ejemplo: _bug report agregado_.
- Confirma el _commit_.
- Pulsa la flecha hacia arriba para sincronizar con la nube.
- Acepta la ventana que configura los comandos `pull` y `push` por primera vez.

Cuando el botón de _commit_ se inhabilita, la sincronización terminó. Regresa a GitHub, entra a **Code** y verifica que la carpeta `.github/ISSUE_TEMPLATE` con el archivo Markdown ya está publicada.

## ¿Qué cambia para los usuarios después de agregar la plantilla?

Al regresar a la pestaña _Issues_ y seleccionar nuevo _issue_, tus colaboradores ya no ven una hoja en blanco. Ahora aparece la opción **bug report** con un botón de inicio.

La plantilla guía al usuario para que llene un título breve, describa el comportamiento esperado, los pasos de reproducción y cualquier dato útil para entender el error. Esto reduce el tiempo que pierdes pidiendo información extra.

La funcionalidad de los _issues_ ya es valiosa por sí sola. Sumarle plantillas eleva la calidad de cada reporte y hace que la colaboración fluya mejor.

## ¿Qué otras plantillas puedo crear además de bug report?

El mismo flujo sirve para cualquier tipo de reporte que quieras estandarizar dentro de tu repositorio. Algunas ideas prácticas:

- **Document report**: para errores en documentación, typos o secciones poco claras.
- **Feature request**: para que los usuarios propongan nuevas funcionalidades.
- **Mejores prácticas**: para sugerencias de optimización o refactorización del código.

Cada plantilla adicional la creas como un nuevo archivo `.md` dentro de `ISSUE_TEMPLATE`. Mientras más opciones ofrezcas, más cómodo será contribuir a tu proyecto y más claridad tendrás tú para mejorar el código que mantienes.

