Si quieres acelerar tu flujo de trabajo en GitHub sin perder tiempo en burocracia, **automatizar GitHub Projects** te permite vincular issues, pull requests y cambios de estado para que todo avance solo mientras tú te concentras en escribir código. Esta guía te muestra cómo hacerlo paso a paso, ideal para quienes gestionan proyectos de software en equipo.

## ¿Cómo vincular un proyecto a tu repositorio en GitHub?

Dentro de tu repositorio, la pestaña _Projects_ aparece vacía hasta que enlazas uno. Antes de hacerlo, conviene renombrar el proyecto desde tu perfil para evitar nombres genéricos como _project sin título_.

- Ve a tu perfil y abre la sección de _Projects_.
- Selecciona el icono de editar y asigna un nombre, por ejemplo _mi proyecto individual_.
- Agrega una descripción y un README que explique las actividades principales.
- Guarda los cambios con el botón superior y regresa al repositorio.

De vuelta en el repositorio, usa la opción _link a project_ y elige el nombre correcto. Cuando aparezca la palomita, tu proyecto queda vinculado y puedes empezar a sumar tareas.

## ¿Cómo creo y organizo actividades dentro del proyecto?

Desde el proyecto vinculado puedes capturar tareas como _actualizar mi proyecto HTML_, _actualizar archivo CSS_ y _actualizar archivo JavaScript_. Cada una se mueve entre tres estados: _todo_, _in progress_ y _done_. Esa columna es la base sobre la que después se construyen métricas y automatizaciones.

> **¿Para qué sirve GitHub Projects?** Es un tablero integrado a tu repositorio que organiza issues y pull requests por estado, responsable y prioridad, para que veas el avance real del proyecto sin salir de GitHub.

## ¿Cómo medir el desempeño con la sección Insights?

En la esquina superior derecha del proyecto está _insights_, donde aparece una **gráfica de status** con cuántas actividades están pendientes, en progreso y terminadas. Esto te ayuda a ver el ritmo del equipo y a identificar a quienes se olvidan de mover sus tarjetas.

Y aquí viene lo interesante: en lugar de pedirle a tu equipo que actualice manualmente cada tarjeta, puedes dejar que GitHub lo haga por ti vía _workflows_.

## ¿Cómo configurar workflows automáticos en GitHub Projects?

Desde los tres puntos del proyecto entras a la categoría de _workflows_, donde GitHub lista las acciones que disparan cambios de estado automáticos .

- _Item closed_: cuando cierras un issue o pull request, la tarjeta pasa a _done_ automáticamente.
- _Code review approved_: al aprobar un pull request, puedes mover la tarea a _done_ sin tocar el tablero.
- Cada flujo se edita con el botón verde _save_ para habilitarlo o cambiar el estado destino.

Con estos flujos activos, tu tablero se actualiza solo cada vez que cierras trabajo en el repositorio.

## ¿Cómo conectar un issue con un pull request usando closes?

La palabra clave para cerrar issues automáticamente es _closes_. El flujo completo se ve así:

1. En tu actividad del proyecto, selecciona los tres puntos y elige _convert to issue_, asociándolo al repositorio.
2. Crea una nueva rama, por ejemplo _amin/17_, desde la sección de _branches_.
3. Agrega tu archivo, como _style.css_, con un comentario inicial y haz commit en esa rama.
4. Abre el pull request y en la descripción escribe: _Agregué el archivo CSS. Closes #17_.

Al hacer esto, GitHub vincula el pull request con el issue y lo muestra en la sección _development_. Cuando el pull request se fusiona, el issue se cierra y la tarjeta del proyecto pasa de _in progress_ a _done_ sin intervención manual .

> **¿Qué hace la palabra closes en un pull request?** Crea un enlace directo entre el pull request y un issue. Al fusionar el pull request, GitHub cierra automáticamente el issue referenciado con _closes #número_.

## ¿Qué pasa después de fusionar el pull request?

Una vez que tu compañero revisa y aprueba el pull request, GitHub lo fusiona, te ofrece eliminar la rama y muestra el issue como cerrado en _development_. Al volver a _projects_, la actividad ya aparece en _done_. Todo el ciclo, desde escribir código hasta actualizar el tablero, queda automatizado.

Vale la pena recordar que aunque aquí todo se hizo desde la web por fines didácticos, en un escenario real harás la creación de ramas, los commits y los pull requests desde la terminal o **VS Code**, que son las herramientas estándar del día a día.

## ¿Hasta dónde puedes expandir los workflows de GitHub?

Los _workflows_ son apenas el primer escalón. Existen extensiones que disparan notificaciones cuando un pull request se cierra y avisan al equipo por:

- Slack, con mensajes en el canal del proyecto.
- Microsoft Teams, integrando alertas en tus chats de trabajo.
- Correo electrónico, para notificar a stakeholders externos.