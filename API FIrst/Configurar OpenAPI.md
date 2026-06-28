Crear una API con ExpressJS y OpenAPI te permite gestionar eficientemente las operaciones CRUD (Crear, Leer, Actualizar, Eliminar) de usuarios. En este proyecto aprenderás a utilizar ExpressJS con JavaScript y la especificación OpenAPI, comenzando con una estructura clara y ordenada desde el principio.

## ¿Cómo iniciar el proyecto con ExpressJS?

Para empezar a configurar tu API, es necesario crear una carpeta específica para tu proyecto. Por ejemplo, puedes utilizar la terminal con el comando `mkdir` seguido del nombre del proyecto:

```bash
mkdir APIFirst
cd APIFirst
```

Es recomendable usar una nomenclatura clara y consistente para identificar tus proyectos fácilmente dentro de un equipo. Por ejemplo, puedes nombrar los microservicios con un formato como `MS-users`.

### Una vez creada la carpeta, inicializa el repositorio usando:

```bash
git init
npm init --yes
```

Esto agrega archivos esenciales para manejar proyectos utilizando GitHub y Node.js.

## ¿Qué dependencias necesito instalar?

Para este proyecto específico, existen algunas dependencias que debes instalar, incluyendo ExpressJS y otras relacionadas con Swagger y YAML para el manejo correcto de OpenAPI. Utiliza el siguiente comando:

```bash
npm install express yamljs swagger-ui-express
```

Estas dependencias son claves para ayudar a estructurar y documentar tu API correctamente.

## ¿Cómo definir la especificación OpenAPI?

Antes de generar código, debes definir claramente la lógica y funcionalidad que tu API tendrá mediante un archivo de especificación OpenAPI en formato YAML. Crea la siguiente estructura básica dentro de la raíz del proyecto en un archivo llamado `openapi.yaml`:

```yaml
openapi: 3.1.1
info:
  version: "1.0"
  title: AppFirst
servers:
  - url: http://localhost:3000
paths:
  /hello:
    get:
      summary: hello world
      responses:
        '200':
          description: Respuesta completa
          content:
            application/json:
              schema:
                type: object
```

Esta especificación funciona como un contrato claro, indicando explícitamente los puntos de entrada, métodos HTTP, tipo de respuestas y el esquema de los datos enviados y recibidos. Definir previamente la API de esta manera permite verificar anticipadamente cómo funcionará la lógica implementada y prevenir futuros errores.

Recuerda que esta etapa es esencial antes de comenzar a escribir código y te permitirá optimizar la comunicación y estructura de tu proyecto antes de la implementación.