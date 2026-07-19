Crear imágenes en Docker desde un archivo Dockerfile marca un paso esencial y más fluido tras superar la fase inicial de configuración. Si ya tienes listo tu Dockerfile, ahora puedes dar vida a tu aplicación construyendo imágenes que podrás compartir o desplegar en distintos entornos.

## ¿Cómo crear una imagen Docker desde el Dockerfile?

La construcción de una imagen Docker se realiza desde la línea de comandos en la misma ubicación donde se encuentra tu archivo Dockerfile. Para confirmarlo, usa el comando básico de Linux `ls`, que verifica que el archivo esté presente en la carpeta. Luego, ejecuta:

```bash
docker build .
```

Este comando indica que la creación se hará utilizando los pasos establecidos en tu Dockerfile desde la posición actual. Docker realizará automáticamente cada instrucción detallada dentro del archivo, por ejemplo, descargar una imagen base o copiar archivos específicos.

### ¿Por qué poner nombre y etiqueta a la imagen Docker?

Al generar una imagen de la forma más rápida, esta aparece por defecto sin nombre ni etiqueta, mostrando _None_ en ambos espacios. Aunque es posible, no es recomendable, ya que dificulta la identificación y gestión de tus imágenes.

Por lo tanto, es mejor práctica etiquetar explícitamente tus imágenes. Para etiquetar la imagen desde un principio, usa el comando:

```bash
docker build -t sitio_web:latest .
```

Usando `-t`, estableces un nombre claro (en este caso "sitio_web") y una etiqueta "latest", que indica la última versión disponible de tu contenido. Esto mejora sustancialmente la administración cuando tienes múltiples versiones o variaciones del mismo sitio o aplicación.

### ¿Cómo eliminar una imagen Docker?

Si creaste una imagen sin etiqueta o con un nombre incorrecto, puedes eliminarla para mantener tu trabajo ordenado. Utiliza para esto el comando siguiente:

```bash
docker rmi -f <identificador_de_la_imagen>
```

El parámetro `-f` representa una eliminación forzada, especialmente útil si existen dependencias involucradas. Tras eliminar, puedes nuevamente recrear tu imagen utilizando el nombre y la etiqueta adecuados.

Te invitamos a practicar continuamente estos comandos y mantener el orden adecuado en tu entorno Docker. Deja en los comentarios cualquier duda adicional que tengas sobre trabajar eficazmente con Dockerfiles e imágenes Docker.

## ¿Como ver las imagenes creadas
```bash
docker images
```