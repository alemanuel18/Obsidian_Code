Trabajar con **plantillas de GitHub Codespaces** te permite levantar entornos preconfigurados para Django, Node, PHP, .NET o Jupyter sin tocar tu máquina local. Aquí verás cómo crear uno desde cero, editar el archivo `devcontainer.json` y conectarlo a Visual Studio Code Desktop para sacarle más provecho al ciclo de vida del entorno.

## ¿Cómo creo un Codespace desde una plantilla en lugar de un repositorio?

Entra a `github.com/codespaces` y verás a la izquierda la lista de tus entornos creados. A la derecha aparece la sección de plantillas con la opción _See all_ para desplegarlas todas .

Al elegir una plantilla, por ejemplo Django con Python, el Codespace se crea sin pedirte el cuestionario habitual. Solo esperas a que termine de configurarse y ya tienes el entorno corriendo.

> **¿Qué ventaja tiene una plantilla sobre crear un Codespace desde un repositorio?** Te ahorra el cuestionario inicial y te entrega un proyecto base ya funcional, ideal para experimentar con tecnologías nuevas sin instalar nada local.

## ¿La URL del Codespace es pública?

Sí. Al copiar la URL del proyecto y abrirla en otra pestaña, verás que es accesible desde Internet . Como cada Codespace corre sobre una máquina virtual expuesta, puedes compartir esa dirección con alguien para mostrar avances en vivo.

## ¿Cómo edito código en tiempo real dentro de un Codespace de Django?

Python no necesita compilarse, así que los cambios se reflejan casi al instante. En la línea 24 del archivo de la plantilla aparece el texto _GitHub Codespaces_ con Django, y al modificarlo el navegador refresca el resultado de inmediato .

Si necesitas reiniciar el servidor, dentro de la terminal presionas `Ctrl C` para terminar la sesión, limpias con `clear` y vuelves a ejecutar el comando con la flecha arriba dos veces. En la línea 27, al editar _Hello World_ y agregar una letra, basta un pequeño refresco de pantalla para ver el cambio aplicado.

## ¿Qué hace el archivo devcontainer.json en un Codespace?

Dentro del proyecto encontrarás una carpeta llamada `.devcontainer` con un archivo JSON que define toda la configuración del entorno . Este archivo mete los archivos y dependencias dentro de un contenedor, una especie de minimáquina virtual donde corre tu Visual Studio en el navegador junto con el lenguaje y las herramientas necesarias.

- En la línea 7 está la configuración base de Python para el proyecto.
- En la línea 20 aparece el listado de extensiones de VS Code que se instalan por defecto.
- En la sección de extensiones puedes agregar nuevas y persistirlas en el contenedor.

## ¿Cómo agrego una extensión de forma permanente al Codespace?

Buscas la extensión deseada, por ejemplo _Live Share_, y la instalas dentro del Codespace. Pero instalarla así no la deja fija: si reinicias el entorno, podrías perderla.

La solución está en el pequeño engrane de la extensión, donde eliges _Add to devcontainer.json_ . Al hacerlo, el archivo de configuración registra que esa plantilla de Django necesita Python y también Live Share, y la extensión queda lista cada vez que levantes el Codespace.

> **¿Para qué sirve add to devcontainer.json?** Sirve para que una extensión instalada manualmente quede registrada en la configuración del contenedor y se reinstale automáticamente la próxima vez que se cree el entorno.

## ¿Cómo abro un Codespace en Visual Studio Code Desktop?

Desde el menú de tres líneas horizontales en la parte superior izquierda eliges _Open in Visual Studio Code Desktop_. Se abre un pop up de confirmación, aceptas y, si es tu primera vez, VS Code te pedirá instalar la extensión **GitHub Codespaces** .

Una vez instalado, abajo aparece una leyenda amarilla indicando que se está abriendo un entorno remoto. La conexión es rápida y la URL del proyecto pasa a ser local.

## ¿Por qué me marca error de puerto en uso al ejecutar Python?

Porque la aplicación sigue corriendo en tu navegador y en VS Code Desktop, y ambas apuntan a la misma máquina virtual. Dos procesos no pueden ocupar el mismo puerto al mismo tiempo.

Para solucionarlo:

1. Regresa al explorador y abre una nueva terminal en el Codespace.
2. Si la terminal no responde, refresca la página para reactivar el entorno.
3. Presiona `Ctrl C` para detener la aplicación que sigue ejecutándose.
4. Vuelve a Visual Studio Code, ejecuta `clear` y levanta de nuevo el servidor.

Con eso liberas el puerto y puedes seguir trabajando desde el escritorio sin perder los cambios. El control de versiones también funciona, así que tus commits llegan al mismo repositorio sin importar si editas en el navegador o en VS Code.

## ¿Qué plantillas de Codespaces existen además de Django?

La galería incluye opciones para distintos stacks que puedes usar para aprender o prototipar:

- Node.js para proyectos JavaScript del lado servidor.
- PHP para entornos web clásicos.
- .NET para aplicaciones del ecosistema Microsoft.
- Django con Python como la usada en este recorrido.
- Jupyter para análisis de datos con Python.

La imagen de **Jupyter** es especialmente útil si estás explorando ciencia de datos: te permite jugar con datasets, aprender Python orientado a esa especialización y, cuando termines, eliminar el Codespace sin haber instalado nada en tu computadora.

La idea de fondo es que abras estas plantillas para revisar cómo están armadas por dentro, leas el `devcontainer.json` de cada una y aprendas a trabajar con tecnologías nuevas sin depender de tu entorno local. ¿Qué plantilla vas a probar primero?