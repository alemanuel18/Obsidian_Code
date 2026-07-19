Dominar Docker implica conocer tanto su interfaz gráfica (Docker Desktop) como su terminal de comandos. Ambas alternativas ofrecen ventajas específicas, así que es ideal familiarizarse con las dos para aprovechar mejor el potencial de Docker.

## ¿Cómo verificar la versión de Docker instalada?

Una acción básica para comprobar nuestra instalación es utilizar la línea de comandos con el comando:

```bash
docker version
```

Este comando confirma que Docker está instalado correctamente y muestra la versión actual y el _build_ correspondiente, asegurando que todo esté listo para trabajar sin complicaciones.

## ¿Qué información relevante aporta `docker info`?

Con el comando:

```bash
docker info
```

Puedes acceder a detalles importantes sobre el hardware disponible o asignado a Docker en tu sistema. Muestra especificaciones relevantes como la memoria, procesador y GPU disponibles, información útil para decidir futuros ajustes en tu equipo.

## ¿Cuáles son los comandos básicos equivalentes a Docker Desktop?

Docker Desktop tiene una interfaz visual amigable, pero es fundamental conocer su equivalente en línea de comandos. Estos son algunos ejemplos clave que puedes memorizar:

- Listar imágenes disponibles:

```bash
docker images
```

- Ver contenedores activos:

```bash
docker ps
```

- Explorar opciones de comandos específicos con ayuda:

```bash
docker images --help
```

Estos comandos ofrecen funcionalidades equivalentes a las categorías gráficas, simplificando el intercambio entre interfaz gráfica y terminal.

## ¿Por qué aprovechar la documentación integrada de Docker?

Docker facilita una documentación integrada extensa y clara a través del comando `docker help` o añadiendo `--help` tras comandos específicos. Es particularmente útil cuando trabajas con comandos complejos como:

- `docker build`: Crea imágenes a partir de archivos Dockerfile.
- `docker run`: Ejecuta contenedores a partir de imágenes disponibles.

Ambos comandos tienen múltiples parámetros, pero la documentación proporcionada al utilizar `--help` facilita enormemente entender cada opción y explicación disponible.

Explorar ambas formas de interactuar con Docker —Docker Desktop y línea de comandos— te permitirá decidir cuál es más adecuada y cómoda según tus preferencias y estilo de trabajo. Te animo a compartir cuál de las dos opciones prefieres utilizar y por qué.