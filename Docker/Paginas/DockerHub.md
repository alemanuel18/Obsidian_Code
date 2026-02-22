***
**Docker Hub** es un **repositorio de contenedores** o un almacén centralizado diseñado para compartir y descargar imágenes de Docker. Se le considera frecuentemente como el "**GitHub de los contenedores**", ya que cumple una función similar de almacenamiento y distribución, pero enfocada exclusivamente en imágenes de contenedores.

Sus características principales, según las fuentes, son:

- **Tipos de Repositorios:** Ofrece tanto repositorios **públicos** como **privados**. Docker Hub es especialmente conocido por ser el repositorio público más grande y utilizado en el ecosistema.
- **Contenido Masivo:** Cuenta con más de **100,000 repositorios** disponibles. En él se pueden encontrar **imágenes oficiales** (mantenidas por los creadores del software) e imágenes creadas por la **comunidad**. Entre las aplicaciones comunes disponibles se encuentran Node.js, Python, MySQL, Postgres y diversas distribuciones de Linux como Ubuntu o Alpine.
- **Gestión de Versiones:** Permite acceder a múltiples versiones de una misma herramienta mediante etiquetas (tags). Por ejemplo, un usuario puede elegir descargar la última versión de Node.js (`latest`) o una específica como la 14 o la 18-alpine.
- **Documentación y Configuración:** Además de alojar los archivos, proporciona las **instrucciones y parámetros de configuración** necesarios para ejecutar los contenedores, como las **variables de entorno** (usuarios, contraseñas, etc.) requeridas para que las aplicaciones funcionen correctamente.

En la práctica, es el lugar de referencia para buscar el nombre exacto de una imagen antes de utilizar comandos como `docker pull` o `docker run` para descargarla a una máquina local

![[Pasted image 20260222133219.png]]