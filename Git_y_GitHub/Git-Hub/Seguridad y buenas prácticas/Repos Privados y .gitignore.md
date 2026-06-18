Proteger tu código en GitHub empieza por dos decisiones simples: hacer privados los repositorios sensibles y configurar un archivo `.gitignore` que evite subir información que no debería salir de tu máquina. Aquí verás cómo aplicar ambas prácticas paso a paso, con ejemplos reales en Visual Studio Code y .NET.

## ¿Cómo cambiar un repositorio público a privado en GitHub?

Los repositorios públicos en GitHub son ideales para mostrar tu trabajo al mundo, pero cuando colaboras con un equipo cerrado o manejas código sensible, lo correcto es restringir el acceso.

Para cambiar la visibilidad de un repositorio existente, sigue esta ruta dentro de GitHub:

1. Entra al repositorio y abre la pestaña _Settings_.
2. Desplázate hasta el final de la categoría _General_, donde encontrarás la _Danger Zone_ en rojo.
3. Selecciona _Change visibility_ y elige la opción _Private_.
4. Confirma dos veces que estás de acuerdo con el cambio.

Una vez aplicado, verás un pequeño candado junto al nombre del repositorio y la etiqueta _Private_ a la derecha. Eso significa que nadie fuera de tu equipo podrá acceder al código.

> **¿Qué pasa con las estrellas y watchers al hacer privado un repositorio?** Se pierden. GitHub te avisa durante el proceso, así que si tu repo ya tenía visibilidad pública con seguidores, esos contadores vuelven a cero al cambiar la visibilidad .

## ¿Para qué sirve el archivo .gitignore en un proyecto?

El archivo `.gitignore` es una lista de patrones que indica a Git qué archivos o carpetas no deben subirse al repositorio. Funciona como un filtro preventivo: todo lo que coincida con esos patrones queda fuera del _commit_ y del _push_.

¿Por qué es tan útil? Porque cada lenguaje y framework genera archivos que no aportan al código fuente. En proyectos de .NET aparecen las carpetas `bin` y `obj`, en Node está `node_modules`, en Python hay archivos de caché, y así con cada tecnología. Subir todo eso ensucia el repositorio y puede romper builds en otras máquinas.

## ¿Cómo crear y usar un .gitignore desde Visual Studio Code?

El flujo dentro de VS Code arranca sincronizando la rama principal antes de tocar archivos. En la terminal escribe `git branch` para confirmar dónde estás, luego `git switch main` y finalmente `git pull` para traer los últimos cambios .

Una vez sincronizado, crea en la raíz del proyecto un archivo llamado `.gitignore`. Dentro puedes escribir patrones como:

- `*.sln` para excluir archivos de solución generados automáticamente.
- `/bin` para ignorar la carpeta de binarios.
- `/obj` para evitar archivos intermedios de compilación.
- `appsettings.json` para no exponer cadenas de conexión.

Cuando un archivo coincide con un patrón, VS Code lo muestra opacado en el explorador. Esa señal visual te confirma que ya no será incluido en el siguiente _commit_.

## ¿Existe una colección oficial de .gitignore por lenguaje?

Sí. GitHub mantiene un repositorio público llamado `github/gitignore` con plantillas listas para casi cualquier tecnología: Node, Python, Java, Go, Rust, Visual Studio y muchas más.

> **¿Dónde encuentro plantillas de .gitignore?** En el repositorio `github/gitignore`. Buscas el archivo de tu stack (por ejemplo `VisualStudio.gitignore` o `Node.gitignore`), abres la vista _Raw_, copias el contenido y lo pegas en tu propio `.gitignore`.

Dentro de la plantilla de Visual Studio, por ejemplo, en la línea 30 ya viene incluida la carpeta `Bin` con mayúscula y minúscula, y lo mismo aplica para `obj`. Eso te ahorra tener que recordar cada ruta específica del lenguaje .

## ¿Por qué nunca debes subir appsettings.json o archivos .env al repositorio?

Los archivos de configuración como `appsettings.json` en .NET o `.env` en Node y Python guardan credenciales, llaves de API y cadenas de conexión a bases de datos. Si suben al repositorio, cualquiera con acceso al código puede ver esa información sensible.

La práctica correcta es agregar estos archivos al `.gitignore` con un comentario claro, por ejemplo:

Elimina este archivo de configuración

appsettings.json

Así, aunque exista localmente y tu aplicación lo use para conectarse a una base de datos, nunca viajará al repositorio remoto.

## ¿Cómo verificar que los archivos quedaron excluidos antes del push?

Antes de subir cambios, ejecuta `git status` en la terminal. Ese comando lista todo lo que será incluido en el próximo _commit_. Si ves ahí archivos que no deberían subirse, ajusta el `.gitignore` antes de continuar.

El flujo seguro queda así:

1. `git status` para revisar qué se va a subir.
2. `git add .` para preparar los cambios válidos.
3. `git commit -m "Nuevo gitignore creado"` para registrar el cambio.
4. `git push` para enviarlo al repositorio remoto.

Al refrescar el repositorio en GitHub, confirmarás que las carpetas `bin`, `obj` y el archivo `appsettings.json` ya no aparecen .

## ¿Cuál es la mejor forma de configurar .gitignore al crear un repositorio?

La opción más limpia es hacerlo desde el inicio. Cuando creas un nuevo repositorio en GitHub, antes de presionar _Create repository_ tienes tres acciones clave:

- Marcar el repositorio como _Private_ si el código es sensible.
- Seleccionar el _owner_ correcto (tu cuenta o una organización).
- Elegir una plantilla en la sección _Add .gitignore_, donde puedes buscar Visual Studio, Node, Python o cualquier otra.

https://github.com/github/gitignore 