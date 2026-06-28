Diseñar una API bajo el enfoque _API First_ implica decidir, antes de escribir lógica, cómo se verán los puntos de entrada, los métodos disponibles y las respuestas posibles. Cuando defines un endpoint en OpenAPI con parámetros obligatorios y múltiples respuestas HTTP, garantizas validaciones claras y un contrato sólido entre quien consume y quien construye la API.

## ¿Cómo se define un endpoint con parámetro de ruta en OpenAPI?

Dentro del archivo OpenAPI, en la sección de _paths_, ya existen rutas como `users` y `hello`. La idea es agregar una nueva ruta que reciba un identificador para localizar un usuario específico .

La ruta queda como `users/{id}` y el primer método que defines es `get`, acompañado de una descripción clara: obtener un usuario por el ID. Esa descripción no es decoración; le dice a cualquier desarrollador o herramienta de documentación qué esperar de ese llamado.

> **¿Qué es API First?** Es un enfoque donde defines el contrato de la API (rutas, métodos, parámetros, respuestas) antes de implementar el código, asegurando consistencia y validaciones desde el diseño.

## ¿Cómo se marca un parámetro como obligatorio y con tipo definido?

Dentro de `parameters` declaras que el dato viaja en el `path`, le asignas el `name` igual a `id`, lo marcas con `required: true` y le defines un `schema` con `type: integer` . Con esos cuatro datos, OpenAPI ya sabe tres cosas críticas: dónde llega el valor, que es indispensable y qué tipo de dato debe respetar.

Esta combinación funciona como una validación temprana. Si alguien intenta llamar al endpoint sin el ID o con un tipo distinto, el contrato lo detecta antes de que la petición llegue a la lógica del servidor.

## ¿Cómo manejar múltiples respuestas HTTP en un mismo endpoint?

Un endpoint rara vez tiene una sola respuesta. Lo realista es contemplar al menos el caso de éxito y el caso donde el recurso no existe.

### Respuesta 200 cuando el usuario existe

En `responses` defines el código `200` con la descripción "usuario encontrado". Dentro agregas `content` con `application/json`, un `schema` de tipo `object` y las propiedades que devuelves: el `id` con su tipo de dato y el `name` como `string` . Así, quien consume la API sabe exactamente qué estructura recibirá cuando todo salga bien.

### Respuesta 404 cuando el usuario no existe

Para cubrir el caso contrario, agregas el código `404` con la descripción "usuario no encontrado". También lleva `content` de tipo `application/json`, un `schema` tipo `object` y una propiedad `message` de tipo `string` que comunica el error de forma legible .

> **¿Por qué definir respuestas 404 en el contrato?** Porque documentar los errores esperados permite que el cliente maneje cada escenario con código específico y no dependa de adivinar qué pasó en el servidor.

## ¿Qué elementos forman el contrato completo de un endpoint?

Al unir todo lo anterior, cada punto de entrada en tu especificación queda compuesto por:

- La ruta con su parámetro de path, por ejemplo `users/{id}`.
- El método HTTP, en este caso `get`, con su descripción.
- Los `parameters` con `name`, `in`, `required` y `schema`.
- Los `responses` con códigos como `200` y `404`, cada uno con su `content`, `schema` y propiedades.

Cada uno de esos bloques aporta información que herramientas de documentación, generadores de código y validadores leen para mantener coherencia entre lo que prometes y lo que entregas.

## ¿Cómo extender el endpoint con un método POST?

El reto natural es agregar un método `post` sobre la misma ruta `users/{id}` para actualizar el nombre del usuario basado en el ID . Eso significa replicar la estructura de `parameters` para el ID, definir un cuerpo de petición con el nuevo `name` y declarar las respuestas posibles, incluyendo el caso exitoso y el escenario donde el usuario no existe.