Diseñar una API antes de escribir código en Express es posible cuando defines el contrato en OpenAPI y dejas que la inteligencia artificial traduzca esa especificación a código funcional. Aquí verás cómo construir y probar endpoints para obtener y actualizar usuarios por ID, respetando reglas de validación declaradas en el archivo `openapi.json`.

## ¿Cómo definir un endpoint POST en OpenAPI antes de codificar?

El reto inicial pedía documentar el método para actualizar un usuario por ID dentro del archivo OpenAPI antes de tocar Express. Esa práctica fija el contrato y evita ambigüedades cuando la herramienta de IA genere el código.

### La especificación necesitaba estos elementos clave:

- Un parámetro `id` marcado como requerido, con su tipo de dato definido.
- Un _request body_ obligatorio con la información a actualizar del usuario.
- Un esquema con campos `name`, `age` y `email`, donde el nombre tiene mínimo 2 caracteres, el correo cumple formato _email_ y la edad mínima es 18.
- Respuestas tipadas: `200` con el usuario actualizado (id, name, age, email) y `404` cuando el usuario no existe.

> **¿Qué es un request body en OpenAPI?** Es el bloque de datos que el cliente envía al servidor en operaciones como POST o PUT. En este caso contiene los campos del usuario que quieres actualizar y puede marcarse como requerido para que la API rechace peticiones vacías.

## ¿Cómo generar el código de Express desde la especificación con IA?

Una vez que el contrato vive en `openapi.json`, basta con seleccionar el bloque de `users` y pedirle a la herramienta de inteligencia artificial que construya el endpoint en `index.js` cumpliendo las reglas de OpenAPI. El prompt apunta directamente a la línea donde se declara el punto de entrada `/users/{id}` para que la IA tenga contexto completo.

### El resultado generado incluye varias piezas:

- Una simulación de base de datos con un _array_ en memoria.
- Un endpoint GET `/users/:id` que convierte el parámetro a entero y busca al usuario.
- Una validación que responde `404` cuando el usuario no existe.
- Un endpoint PUT (o POST según el diseño) que localiza al usuario, aplica el _update_ y devuelve el JSON actualizado.

Un detalle a tener presente es que la validación del esquema ocurre a nivel API, pero también necesitas verificar la existencia del usuario en tu fuente de datos, que aquí es solo un _array_ en memoria.

## ¿Por qué revisar el código que entrega la IA?

El mismo prompt puede dar resultados distintos si cambias valores o si la indicación no es clara. Por eso conviene leer línea por línea lo que la herramienta propone, confirmar que respeta el contrato y ajustar lo que haga falta. Si quieres mejorar tus instrucciones, el curso de _Prompt Engineering_ en Platzi profundiza en esa habilidad.

## ¿Cómo simular la base de datos para probar la API?

Como el foco está en el diseño desde OpenAPI y no en la persistencia, la solución usa un _array_ con usuarios precargados que cumplen el esquema: un id, un nombre, una edad mayor a 18 y un correo válido. Esa estructura permite probar los endpoints sin levantar un motor de base de datos.

Entre los usuarios de prueba aparece María García con id 2, que sirve para validar tanto la lectura como la actualización.

## ¿Cómo probar los endpoints en Swagger?

Con el servidor corriendo y sin errores en la terminal, la documentación generada por Swagger muestra los dos recursos listos: obtener un usuario por ID y actualizar uno por ID. Desde ahí puedes ejecutar peticiones reales contra la API.

### Estas son las pruebas que confirman que el contrato se cumple:

1. GET con id `1` devuelve solo el id y el nombre, tal como definiste en la respuesta `200` del OpenAPI.
2. GET con id `20` responde `404` con el mensaje de usuario no encontrado.
3. PUT con id `2` enviando un payload válido actualiza a María García por el nuevo valor y la siguiente lectura confirma el cambio en memoria.
4. PUT con id `1` enviando un nombre de solo tres caracteres devuelve `400 Bad Request` porque rompe la regla de longitud mínima.

> **¿Qué diferencia hay entre un 400 y un 404 en una API REST?** Un `400` indica que la petición está mal formada o no cumple las reglas de validación, como un nombre demasiado corto. Un `404` significa que el recurso solicitado no existe, por ejemplo un usuario con id 20 que no está en la base de datos.

La lógica de validación queda lista sin haber escrito reglas manuales en Express: la especificación OpenAPI dicta el comportamiento y la IA lo traduce a código que respeta esos límites. ¿Qué endpoint vas a documentar primero en tu próximo proyecto?