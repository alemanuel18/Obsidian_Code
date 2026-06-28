Cuando construyes una API con Express.js, validar manualmente cada petición y respuesta consume tiempo y abre la puerta a errores silenciosos. Con **Express OpenAPI Validator** puedes automatizar esa validación contra tu archivo de especificación y garantizar que tu API cumpla el contrato definido, sin escribir validaciones a mano.

Esta herramienta encaja perfecto si ya documentas tu API con OpenAPI y quieres que múltiples equipos consuman la información bajo un mismo estándar.

## Qué hace Express OpenAPI Validator y por qué usarlo

Es un _middleware_ que se conecta a Express e intercepta cada petición y respuesta para compararlas contra tu spec de OpenAPI. Si algo no cumple el contrato, devuelve un error claro antes de que llegue a tu lógica de negocio.

Entre las ventajas que obtienes al integrarlo:

- Validación automática de tipos, formatos y esquemas declarados en el spec.
- Documentación viva que también sirve para probar la API desde la misma herramienta.
- Estandarización para equipos que consumen tu API en distintos lenguajes.

> **¿Qué es Express OpenAPI Validator?** Es un middleware que valida automáticamente las peticiones y respuestas de tu API en Express contra las reglas declaradas en un archivo OpenAPI.

Y aquí viene lo interesante: aunque trabajemos con Express y JavaScript, OpenAPI es una especificación agnóstica. Vas a encontrar herramientas equivalentes en prácticamente cualquier lenguaje .

## Cómo instalo y configuro el validador en Express

El primer paso ocurre en la terminal. Instalas el paquete con `npm install express-openapi-validator` y lo importas en tu archivo principal.

### Importar el paquete y declarar la constante

En tu editor, agrega el import y crea una constante llamada `OpenApiValidator` que apunte al paquete recién instalado. Mantén el orden jerárquico de tu archivo: imports arriba, declaración de Express, recursos como la documentación, y al final el middleware del validador.

### Registrar el middleware con app.use

Después del bloque de docs, llama a `app.use` con la configuración del validador. La configuración por defecto funciona, pero necesitas añadir `ignorePaths` para que el validador no intente revisar la ruta de la documentación, que no forma parte del contrato.

El orden recomendado en tu archivo queda así:

1. Imports y constantes.
2. Inicialización de Express.
3. Configuración de docs.
4. `app.use` del OpenAPI Validator con `ignorePaths`.
5. Middleware de manejo de errores.

## Cómo manejo los errores que devuelve el validador

Un validador sin manejo de errores te deja con respuestas crudas y poco útiles. Por eso conviene agregar otro middleware específico para errores, justo después del validador .

Este middleware recibe cuatro parámetros: `error`, `request`, `response` y `next`. Esa firma con cuatro argumentos es la que Express reconoce como manejador de errores.

### Dentro de él, defines la respuesta así:

- `res.status` recibe `error.status` o un fallback a 500.
- El cuerpo incluye un `message` y el `error` con la información del problema.

> **¿Por qué necesito un middleware aparte para errores?** Porque Express identifica los manejadores de errores por tener cuatro parámetros y permite separar la lógica de validación de la presentación del fallo.

Con esa estructura, cualquier petición que rompa el contrato se devuelve con un mensaje legible en lugar de un _stack trace_ confuso.

## Qué pasa cuando pruebo la API con el validador activo

Levantas el servidor con `npm run dev`. Si la consola no muestra errores, la inicialización fue limpia; presta atención a _typos_ o paquetes faltantes porque normalmente aparecen ahí.

Al entrar a la documentación, todo sigue funcionando. Pero si visitas la ruta raíz `/`, que antes mostraba un error genérico, ahora recibes una respuesta amigable: un `message: not found` indicando que el path `/` no existe en el contrato.

Este detalle importa mucho. Sin el validador, podrías pensar que el problema es el método HTTP, que quizá deberías probar con POST, PUT o DELETE. Con el validador, queda claro que esa ruta simplemente no está declarada en el spec.

Las rutas que sí existen, como `/hello`, siguen respondiendo sin problema . Esa es la confirmación de que el middleware solo bloquea lo que no cumple el contrato.

> **¿Qué error muestra el validador si una ruta no existe?** Devuelve un mensaje not found indicando que el path solicitado no está declarado en la especificación OpenAPI.

## Cómo encaja esto en un flujo de trabajo con OpenAPI

La ventaja real aparece cuando combinas tres piezas: el spec de OpenAPI como contrato, la documentación interactiva generada automáticamente y el validador que aplica ese contrato en tiempo de ejecución.

Vas definiendo specs de forma gradual, construyes la API alrededor de ellos y obtienes documentación y validación sin escribir código adicional. Para equipos distribuidos, esto significa que todos consumen la misma fuente de verdad.

Si quieres profundizar en cómo funcionan los middlewares y el patrón de `next` dentro de Express, el curso de Express.js en Platzi cubre esos detalles a fondo.