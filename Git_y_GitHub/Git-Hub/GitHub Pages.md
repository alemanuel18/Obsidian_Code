Si te interesa el desarrollo _front end_, existe una funcionalidad dentro de GitHub que te permite publicar sitios web de forma gratuita y accesible para cualquier persona en el mundo. **GitHub Pages** convierte un repositorio en un servidor de alojamiento web, sin importar si tu sitio es estático o dinámico, y todo funciona integrado con el flujo de trabajo habitual de Git.

## ¿Cómo funciona GitHub Pages y por qué es tan útil?

GitHub Pages no es un entorno aislado. Trabajas directamente sobre un **repositorio de GitHub**, lo que significa que cada cambio que hagas en tu código se refleja de manera casi inmediata en tu sitio publicado. Esto lo convierte en una herramienta ideal para portafolios, páginas personales o proyectos de práctica.

Un dato importante: por defecto, **todas las GitHub Pages son públicas** . La única forma de mantener una página privada es mediante planes empresariales. Para la mayoría de casos de uso personal o educativo, el repositorio público funciona perfectamente.

## ¿Qué pasos seguir para crear tu repositorio de GitHub Pages?

El proceso comienza en la página **pages.github.com** , donde encontrarás un tutorial básico. La regla fundamental es que el repositorio debe llamarse exactamente con el formato `username.github.io` . Es decir, tu nombre de usuario seguido de `.github.io`.

- Crea un nuevo repositorio con el nombre `tunombredeusuario.github.io`.
- Hazlo público y agrega un archivo README.
- Copia la dirección SSH desde el botón _code_ del repositorio.
- Clona el repositorio en tu entorno local con `git clone` .

## ¿Cómo agregar contenido y la carpeta docs?

Una vez clonado el repositorio, ábrelo en **Visual Studio Code** con el comando `code .` . Lo siguiente es colocar los archivos de tu sitio web dentro de una carpeta con un nombre específico: **docs** . Esta palabra es obligatoria, ya que GitHub Pages la reconoce como la fuente del contenido a desplegar.

Puedes usar cualquier archivo HTML que desees. En el ejemplo se utiliza una plantilla con un `index.html` y una carpeta de _assets_ . Lo valioso es que puedes personalizar completamente el contenido: agregar tus redes sociales, tu imagen y cualquier información que quieras compartir.

## ¿Cómo subir los cambios y configurar el despliegue?

Con la carpeta **docs** lista, el siguiente paso es subir los cambios al repositorio remoto. Desde la terminal ejecuta los siguientes comandos :

bash git add . git commit -m "plantilla HTML" git push

Una vez que los cambios estén en GitHub, dirígete a **Settings** del repositorio. En la columna izquierda selecciona la categoría **Pages** . El asistente te preguntará desde dónde desplegar la información:

- Selecciona _Deploy from a branch_ en lugar de GitHub Actions.
- Elige la rama **Main** como fuente.
- Selecciona la carpeta **/docs** como directorio raíz del sitio .
- Guarda los cambios.

Cuando aparezca el mensaje **GitHub Pages Source Saved**, regresa a la página principal y luego vuelve a entrar a Settings > Pages. Verás un nuevo mensaje indicando que **tu sitio está en vivo** junto con la URL pública .

## ¿Qué son los dominios personalizados en GitHub Pages?

Dentro de la configuración de Pages existe una sección llamada **Custom Domain** . Esta funcionalidad te permite asociar un dominio propio, como `tunombre.com`, a tu GitHub Page. De esta forma, la URL deja de ser larga y pasa a corresponder con un nombre de dominio personalizado, lo cual es ideal si quieres darle un aspecto más profesional a tu presencia en línea.

Cada modificación que realices en la plantilla HTML dentro de la carpeta docs se verá reflejada de forma casi inmediata en tu página publicada . Esto hace que el ciclo de desarrollo y despliegue sea extremadamente ágil.

Si ya creaste tu GitHub Page, compártela para que otros puedan ver el resultado de tu trabajo y te den retroalimentación sobre el diseño y contenido que elegiste.