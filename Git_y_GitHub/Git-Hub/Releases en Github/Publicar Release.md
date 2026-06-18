Publicar un _release_ en GitHub te permite versionar tu código y distribuirlo como paquete instalable. Aquí verás cómo crear un _release_ con _tag_, adjuntar binarios y consumir ese paquete pip desde una aplicación Python local, ideal si estás aprendiendo a empaquetar y distribuir software propio.

## ¿Cómo se crea un nuevo release en GitHub?

Dentro de tu repositorio, busca la sección **Releases** a la derecha y selecciona la opción para crear uno nuevo. El formulario te pedirá un _tag_, que es la versión que quieras publicar.

En este caso usamos `v0.1.0`, tomando como base la rama `main`. Si no recuerdas qué versión declaraste en tu proyecto, vuelve a Visual Studio Code y revisa la versión configurada ahí mismo. Mantener coherencia entre la versión del proyecto y el _tag_ del _release_ evita confusiones futuras .

> **¿Qué es un tag en GitHub?** Es una etiqueta que marca un punto específico del historial del repositorio, normalmente asociado a una versión como `v0.1.0`. Sirve como referencia inmutable para tus _releases_.

En el campo **release title** se acostumbra reutilizar el mismo _tag_ como título, así que escribe `v0.1.0`. La descripción puede quedar vacía si es tu primera prueba.

## ¿Debo subir binarios o solo el código fuente?

Si no te sientes seguro publicando solamente el código fuente, GitHub te permite adjuntar binarios. Dentro de tu proyecto, los binarios viven en la carpeta `dist` y suelen tener dos formatos:

- Archivo `.tar.gz`, una distribución comprimida del código fuente.
- Archivo `.whl`, el formato _wheel_ recomendado para instalar con pip.

Selecciónalos, ábrelos y quedarán adjuntos al _release_. Si esta es tu primera versión estable, no marques _pre-release_ y publica directamente con el botón correspondiente .

## ¿Cómo consumir tu paquete pip desde otra aplicación Python?

Una vez publicado el _release_, cambia de lugar de trabajo y abre otro repositorio donde vivirá la aplicación que consumirá el paquete. Desde la terminal escribe `code .` para abrir Visual Studio Code en esa carpeta.

Dentro del repositorio crea una carpeta llamada `app` y, dentro de ella, un archivo `app.py`. Esa será tu aplicación cliente.

## ¿Cómo instalo un paquete pip desde una URL de GitHub?

Ve a tu _release_ publicado, haz clic derecho sobre el archivo `.whl` y copia el enlace. En la terminal ejecuta:

bash pip3 install <URL-del-archivo-whl>

Eso descargará e instalará tu paquete directamente desde GitHub, sin necesidad de subirlo a PyPI todavía. Para verificar que quedó instalado, usa:

bash pip3 list

El comando muestra en orden alfabético todos los paquetes disponibles en tu entorno. Ahí debería aparecer tu paquete con la versión `0.1.0` .

> **¿Para qué sirve pip3 list?** Lista todos los paquetes instalados en tu entorno Python con sus versiones. Es la forma rápida de confirmar que una instalación se completó correctamente.

## ¿Cómo importo y uso el paquete en mi código?

En `app.py` importa el módulo y usa la función que expusiste en tu paquete. Si tu paquete se llama `tercer_repo` y contiene un método `saludo`, el código queda así:

python from tercer_repo import saludo

print(saludo("Platzi"))

Desde la terminal entra a la carpeta con `cd app` y ejecuta `python3 app.py`. La salida será el mensaje definido en tu paquete, por ejemplo: `Hola, Platzi, desde el repo de Platzi` .

Acabas de cerrar el ciclo: creaste un paquete, lo publicaste como _release_ en GitHub y lo consumiste desde una aplicación independiente. Ese mismo flujo aplica si trabajas con _NuGet_ en .NET o con _NPM_ en Node, solo cambian las herramientas de empaquetado y los comandos de instalación.

## ¿Qué habilidades y conceptos clave dominas tras este flujo?

Este ejercicio te deja varias capacidades concretas listas para reutilizar en otros proyectos.

- Versionado semántico con _tags_ tipo `v0.1.0` para marcar puntos del historial.
- Publicación de _releases_ en GitHub con binarios `.whl` y `.tar.gz`.
- Instalación de paquetes pip desde URLs externas, sin depender de PyPI.
- Verificación de entornos Python con `pip3 list`.
- Importación y consumo de tu propio paquete en una aplicación cliente.