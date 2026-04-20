***
Los **volúmenes** son una herramienta de Docker que permite **almacenar datos de manera persistente** fuera del sistema de archivos del contenedor. Son esenciales, especialmente para las bases de datos, porque resuelven el problema de la naturaleza efímera de los contenedores.

A continuación se detalla qué son y por qué su uso es obligatorio al trabajar con datos:

¿Qué son los volúmenes?

Un volumen es un mecanismo que permite **montar una carpeta del sistema de archivos del contenedor en la máquina física (host)**. De esta manera, aunque el contenedor sea una unidad aislada con su propio sistema de archivos, ciertos datos específicos se escriben directamente en el disco duro de la computadora anfitriona.

Existen tres tipos principales de volúmenes:

- **Anónimos:** Docker decide dónde guardarlos, pero son difíciles de referenciar para otros contenedores.
- **De anfitrión (Bind Mounts):** El usuario decide exactamente qué carpeta de su computadora se conecta con qué carpeta del contenedor.
- **Nombrados:** Son administrados por Docker, pero el usuario les asigna un nombre para poder reutilizarlos fácilmente en otros contenedores o versiones de la misma imagen.

¿Por qué son esenciales para las bases de datos?

Sin volúmenes, el uso de bases de datos en Docker sería impracticable por las siguientes razones:

1. **Persistencia de datos:** Por defecto, cuando un contenedor se elimina, todos los archivos que estaban dentro de su sistema de archivos (incluyendo las tablas y registros de una base de datos) desaparecen para siempre. Los volúmenes aseguran que la información **persista en el tiempo**, incluso si el contenedor es detenido o borrado.
2. **Mantenimiento y actualizaciones:** Permiten actualizar la versión de una base de datos (por ejemplo, pasar de MongoDB 5 a 6) sin perder la información. Basta con borrar el contenedor viejo y crear uno nuevo que apunte al mismo volumen donde están los datos.
3. **Rutas específicas por motor:** Cada base de datos tiene una ruta interna donde guarda su información. Al usar volúmenes, mapeamos esa ruta interna a nuestro host para salvar los datos:
    - **MongoDB:** Guarda sus datos en `/data/db`.
    - **MySQL:** Los almacena en `/var/lib/mysql`.
    - **Postgres:** Utiliza `/var/lib/postgresql/data`.

En la práctica, al usar herramientas como **Docker Compose**, se define una propiedad de `volumes` para que el motor de base de datos escriba en un almacenamiento seguro y duradero, permitiendo que la aplicación mantenga su estado tras reinicios o despliegues.