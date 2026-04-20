***
Los comandos básicos de Docker se dividen principalmente en la gestión de imágenes, contenedores, redes y la automatización con Docker Compose. Estos permiten controlar todo el ciclo de vida de una aplicación, desde su empaquetado hasta su ejecución.

# Gestión de Imágenes

Las imágenes son las plantillas inmutables que contienen el código y las dependencias de tu aplicación.

- **docker pull imagen**: Descarga una imagen desde un repositorio como Docker Hub. Si no se especifica una versión con etiquetas (tags), descarga la última por defecto (`latest`).
-  **docker pull imagen:version**
- **docker images**: Muestra un listado de todas las imágenes que has descargado o creado en tu máquina física.
- **docker image rm <nombre/ID>**: Elimina una imagen específica de tu almacenamiento local.
- **docker build -t <nombre> .**: Crea una nueva imagen personalizada a partir de un archivo **Dockerfile** ubicado en el directorio actual.

# Gestión de Contenedores

Los contenedores son las instancias en ejecución de las imágenes.

- **docker create <imagen>**: Crea un nuevo contenedor basado en una imagen, pero no lo inicia automáticamente.
- **docker create  --name (nombre) <imagen>**
- **docker start <nombre/ID>**: Inicia un contenedor que ya ha sido creado previamente.
- **docker stop <nombre/ID>**: Detiene de manera elegante la ejecución de un contenedor activo.
- **docker rm <nombre/ID>**: Elimina un contenedor. El contenedor debe estar detenido para poder borrarlo.
- **docker ps**: Lista únicamente los contenedores que están **corriendo** en ese momento.
- **docker ps -a**: Muestra **todos** los contenedores del sistema, incluyendo aquellos que están detenidos o salidos.
- **docker run <imagen>**: Es un comando que combina tres acciones: busca la imagen (si no la tiene, la descarga), crea el contenedor y lo inicia inmediatamente.
    - **docker run -d**: Ejecuta el contenedor en segundo plano (modo _detached_).
    - **docker run -p <puerto_host>:<puerto_contenedor>**: Mapea un puerto de tu computadora física a un puerto interno del contenedor.
- **docker logs <nombre/ID>**: Muestra los registros o mensajes de salida generados por la aplicación dentro del contenedor. Usar `--follow` permite ver los logs en tiempo real.

# Gestión de Redes

Las redes permiten que los contenedores se comuniquen entre sí en un entorno aislado.

- **docker network ls**: Lista todas las redes configuradas en Docker.
- **docker network create <nombre>**: Crea una nueva red interna para agrupar contenedores.
- **docker network rm <nombre>**: Elimina una red específica.

# Docker Compose

Se utiliza para gestionar aplicaciones que dependen de múltiples contenedores (como una app web y su base de datos) mediante un archivo `docker-compose.yml`.

- **docker compose up**: Construye, crea e inicia todos los servicios definidos en el archivo de configuración con un solo comando.
- **docker compose down**: Detiene y **elimina** todos los contenedores y redes creados por `up`, realizando una limpieza completa del entorno.