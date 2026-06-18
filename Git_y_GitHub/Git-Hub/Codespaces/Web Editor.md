Dentro de cualquier repositorio de GitHub existe un editor de texto integrado al que puedes acceder con solo presionar un punto (".") en tu teclado. Esta herramienta, conocida como **GitHub Dev Editor**, ofrece una interfaz visual muy similar a Visual Studio Code directamente en el navegador, sin necesidad de instalar nada ni consumir recursos en la nube. Aunque puede pasar desapercibida durante años, resulta extremadamente útil para correcciones rápidas.

## ¿Cómo se accede al GitHub Dev Editor?

Desde la portada de cualquier repositorio o cualquier ubicación dentro de él, basta con **presionar la tecla punto (".")** para que GitHub redirija automáticamente a un editor web . En cuestión de segundos, el entorno carga todos los archivos del proyecto con una interfaz familiar: explorador de archivos a la izquierda, editor con números de línea al centro y _preview_ de archivos como el _readme_.

Una vez dentro, puedes:

- Editar cualquier archivo del proyecto, no solo el _readme_.
- Ver los cambios reflejados en el ícono de control de versiones.
- Realizar un _commit_ y _push_ directamente desde el editor con un mensaje descriptivo .

El flujo es simple: abres el editor, haces la modificación, cierras la pestaña del archivo para guardar y luego ejecutas el _commit_. Para regresar al repositorio original, puedes ir al menú de tres líneas horizontales y seleccionar **"Go to repository"** , lo que abre una nueva pestaña donde confirmas que los cambios ya están aplicados.

## ¿Cuál es la diferencia entre el Dev Editor y un CodeSpace?

Aunque la interfaz del Dev Editor se parece mucho a la de un **GitHub CodeSpace**, la diferencia es fundamental: el Dev Editor es **únicamente un editor de texto** . No cuenta con terminal integrada ni permite compilar, ejecutar o probar código. Si intentas abrir una terminal, el propio editor te sugiere migrar a un CodeSpace.

En cambio, un CodeSpace es una **instancia completa en la nube** que funciona como un entorno de desarrollo remoto. Incluye terminal, extensiones, compiladores y todo lo necesario para ejecutar un proyecto de principio a fin.

## ¿Cuándo conviene usar cada herramienta?

La decisión depende de dos factores: **la complejidad de la tarea y el costo** .

- **Dev Editor:** ideal para corregir errores ortográficos en la documentación, eliminar código comentado que se dejó por error o modificar unas pocas líneas. Es gratuito y no consume recursos.
- **CodeSpace:** necesario cuando requieres compilar, ejecutar pruebas o trabajar con un entorno de desarrollo completo. Tiene un costo asociado que se genera en tu cuenta una vez que superas las **horas gratuitas mensuales** incluidas en tu plan.

## ¿Para qué casos prácticos resulta más útil el Dev Editor?

El GitHub Dev Editor brilla en situaciones cotidianas donde abrir un entorno completo sería excesivo :

- Corregir un comentario adicional que quedó en el código.
- Arreglar un error ortográfico en la documentación del proyecto.
- Editar archivos de configuración con cambios menores.
- Revisar visualmente la estructura de varios archivos sin descargar el repositorio.

En lugar de editar el archivo "en crudo" usando el pequeño ícono de lápiz que GitHub ofrece por defecto, el Dev Editor proporciona una experiencia visual mucho más cómoda con resaltado de sintaxis y navegación entre archivos.

El balance entre estas dos herramientas —**edición rápida gratuita** con el Dev Editor y **entorno de desarrollo remoto** con CodeSpaces— representa el cierre natural del trabajo colaborativo en GitHub. Si ya conocías el editor de lápiz pero no este atajo, pruébalo en tu próximo repositorio y comparte qué tan útil te resulta para tus flujos de trabajo diarios.