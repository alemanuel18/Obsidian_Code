***
Las imágenes son **archivos inmutables** que sirven como plantillas para crear contenedores.

- Contienen todo lo necesario para que una aplicación funcione: código, tiempo de ejecución, herramientas del sistema y bibliotecas.
- Están construidas por **capas** (procedentes del Dockerfile), lo que permite optimizar el espacio en disco, ya que si dos imágenes comparten capas iguales, no se descargan dos veces.
- Son **portables**, lo que significa que se pueden compartir fácilmente entre desarrolladores y equipos de operaciones a través de repositorios como **Docker Hub**.

# Comandos
![[Comandos Basicos#Gestión de Imágenes]]
# Conseguir imagenes 
Puedes conseguir imagenes pre echas en docker hub
![[DockerHub]]