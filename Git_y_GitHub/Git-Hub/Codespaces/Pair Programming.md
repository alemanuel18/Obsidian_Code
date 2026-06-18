Colaborar en código sin que nadie toque tu equipo es posible gracias a la combinación de **GitHub Codespaces y la extensión Live Share**. Aquí aprendes a invitar a otra persona a tu entorno virtual, editar en tiempo real y cerrar la sesión sin dejar rastro en tu máquina local.

Esta guía es útil si trabajas con Django, Python u otras tecnologías en VS Code y quieres hacer _pair programming_ aprovechando la nube.

## Qué es Live Share y por qué usarlo dentro de Codespaces

Live Share es la extensión que abre un puente de comunicación para que un colaborador entre a tu entorno de trabajo, edite líneas y, junto contigo, decida qué se queda como producto final antes de un commit.

Dentro de Codespaces, esta extensión vive en la categoría _Codespaces_ del panel de extensiones de VS Code. Si la dejaste preconfigurada en tu archivo `devcontainer.json`, aparecerá lista para usarse al abrir el entorno.

> **¿Qué es pair programming?** Es una práctica donde dos desarrolladores trabajan sobre el mismo código al mismo tiempo. Uno escribe, el otro revisa y sugiere, y ambos acuerdan los cambios finales .

## Cómo iniciar una sesión de Live Share

Desde el explorador de archivos en VS Code, baja hasta la sección **Live Share** y haz clic. Se genera un enlace de invitación que se copia automáticamente a tu _clipboard_.

Envía ese enlace a tu colaborador por el medio que prefieras. Cuando lo abra, verá dos opciones:

- Abrirlo directamente en Visual Studio Code de escritorio.
- Continuar en la web con VS Code Web.

Lo ideal es que tu invitado lo abra desde VS Code de escritorio para optimizar recursos. Si entra como anónimo, puede registrarse con un alias temporal tipo _Invitado 2_.

## Cómo se ve la colaboración en tiempo real

Una vez conectado, VS Code te notifica que el invitado entró a la sesión. En la pantalla aparece su cursor con su nombre y puedes seguir su actividad línea por línea.

Las ediciones fluyen en ambos sentidos casi en tiempo real. Tú ves lo que él modifica y él ve lo que tú escribes. Si quieres mantenerte pasivo y solo revisar sus sugerencias, puedes hacerlo sin interrumpir.

> **¿Quién se queda con el crédito de los cambios en Live Share?** El dueño del Codespace. Como las ediciones ocurren en tu entorno, el commit queda a tu nombre, pero VS Code añade una nota indicando que el trabajo se hizo en colaboración con tu invitado .

## Qué pasa si cierras el Codespace durante una sesión

El entorno es virtual y vive en la nube, así que si cierras tu Codespace, la sesión del invitado también termina. Es una protección natural: nadie puede seguir trabajando en tu espacio sin tu presencia.

Si vuelves a abrir el Codespace y no tienes la extensión declarada en `devcontainer.json`, puede que necesites instalarla de nuevo. Por eso conviene dejarla preconfigurada desde el principio.

## Cómo cerrar correctamente la sesión y el Codespace

Cuando termines de colaborar, baja a la sección **Share** y elige la opción **Stop collaboration session**. Eso saca a todos los participantes y devuelve tu trabajo a un estado individual.

Después, ve a `github.com/codespaces` para revisar tu plantilla. Lo recomendado es entrar al menú de los tres puntos y **eliminar la plantilla** una vez concluido el trabajo, porque sigue siendo un entorno en la nube que consume recursos.

## Beneficios concretos de colaborar con Codespaces y Live Share

Trabajar así tiene ventajas que se notan desde la primera sesión:

- Permites que una o varias personas entren a un entorno virtual sin tocar tu equipo local.
- Pueden unificar el trabajo de todo el equipo en un solo commit.
- Aíslas tu entorno de desarrollo personal del resto del equipo.
- Configuras extensiones específicas (Markdown, Python, C#, Live Share) y las mandas al entorno virtual desde `devcontainer.json`.

El _pair programming_ suele ser una de las prácticas que más cuesta adoptar a los desarrolladores. Tener un entorno en la nube donde puedes invitar amigos, editar juntos y cerrar todo al final reduce esa fricción.