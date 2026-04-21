Dominar el manejo eficiente de archivos es clave en sistemas Linux. Dos procesos fundamentales, pero distintos, son el **empaquetado** y la **compresión**. Si bien empaquetar significa reunir varios archivos en uno solo para facilitar su distribución, comprimir implica reducir su tamaño eliminando redundancias de datos.

# ¿Qué significa empaquetar archivos y cuándo es útil?

**Empaquetar** consiste en combinar múltiples archivos o carpetas en un único paquete que el sistema operativo reconocerá como un solo archivo. Un ejemplo típico ocurre al descargar archivos comprimidos en formato ZIP desde un navegador; estos son archivos empaquetados.

En entornos Linux, el empaquetador habitual es **TAR**. Para empaquetar archivos, utilizamos comandos específicos en la terminal:

`tar -cvf textos.tar textos`

Este procedimiento crea un archivo `.tar` que contiene la carpeta especificada, en este caso "textos".

# ¿Cómo comprimir archivos para ahorrar espacio?

La **compresión** reduce significativamente el tamaño de un archivo eliminando datos redundantes. El estándar más común en terminal Linux es **gzip**.

A continuación, un ejemplo práctico para comprimir el archivo previamente empaquetado:

`gzip textos.tar`

Este comando comprimirá el archivo generando uno nuevo con extensión `.tar.gz`, resultando en un archivo mucho más pequeño.

# ¿Cómo descomprimir y desempaquetar archivos correctamente?

Cuando recibimos un archivo `.tar.gz`, necesitamos primero **descomprimirlo** y luego **desempaquetarlo**. Son procesos independientes que hacemos en dos pasos:

1. **Descomprimir con gzip usando el comando gunzip:**

`gunzip textos.tar.gz`

2. **Desempaquetar el archivo TAR resultante:**

`tar -xvf textos.tar`

TAR también permite simplificar estos pasos añadiendo la opción `z` para realizar ambas operaciones de una sola vez:

`tar -xzvf textos.tar.gz`

Ahora, recuerda que tanto empaquetar como comprimir son técnicas independientes. Puedes crear un paquete sin comprimir o comprimir archivos individuales sin empaquetarlos.