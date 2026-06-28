Definir un endpoint POST en OpenAPI antes de escribir código en Express te permite validar datos automáticamente, sin escribir validadores manuales para nombre, edad o correo. Si trabajas con Node.js y buscas APIs más limpias, este flujo te ahorra horas de lógica repetitiva.

La idea central es simple: el contrato que defines en el archivo OpenAPI se convierte en la fuente de verdad. Express solo recibe la petición y responde, mientras un _validator_ intercepta cualquier dato que no cumpla las reglas.

## ¿Cómo se define un endpoint POST en OpenAPI?

Todo arranca en el archivo OpenAPI, donde describes el nuevo _path_ `/users` con el método `post` antes de tocar Express.

Dentro de ese path declaras un `summary` corto como crear un nuevo usuario y un `requestBody` marcado como `required: true`. Después defines el `content` con `application/json` y, dentro, un `schema` de tipo `object`.

### El `schema` necesita dos bloques clave:

- `required`: lista los campos obligatorios, en este caso `name`, `age` y `email`.
- `properties`: describe el tipo y las reglas de cada campo.

Para `name` defines `type: string` con `minLength: 2`. Para `age`, `type: integer` con `minimum: 18`. Para `email`, `type: string` con `format: email`. Esas tres reglas reemplazan validadores manuales que normalmente escribirías en JavaScript.

> **¿Qué hace el campo required en OpenAPI?** Marca qué propiedades del objeto son obligatorias. Si una petición llega sin alguna de ellas, el _validator_ responde con un error 400 antes de llegar a tu lógica.

## ¿Cómo se documenta la respuesta 201?

En el bloque `responses` agregas el código `201` con su `description` y su `content` en `application/json`. Aquí está el detalle que suele romperse: las propiedades de la respuesta deben ir dentro de un `schema` con `type: object`, no sueltas. Si las pones fuera, el _validator_ lanza un error de esquema al levantar el servidor.

La respuesta declara cuatro propiedades: `id` como string, `name` como string, `age` como integer y `email` como string. Así el consumidor de la API sabe exactamente qué recibir.

## ¿Cómo se conecta OpenAPI con Express?

En el archivo de Express creas la ruta con `app.post('/users', (req, res) => { ... })`. Antes, en la parte superior, agregas el _middleware_ `app.use(express.json())` para que el cuerpo JSON llegue parseado a `req.body`.

Dentro del _handler_ desestructuras `name`, `age` y `email` desde `req.body`. Y aquí viene lo interesante: no escribes ni un solo `if` para validar. El _validator_ conectado a OpenAPI ya rechazó cualquier petición que no cumpla el contrato.

### El cuerpo del _handler_ queda mínimo:

```js 
app.post('/users', (req, res) => { 
	const { name, age, email } = req.body; 
	const newUser = { 
		id: Date.now().toString(), name, age, email 
	}; 
	res.status(201).json(newUser); 
});
```

El `id` se genera con `Date.now().toString()` como ejemplo. En un proyecto real, esa lógica conecta con Prisma y una base de datos Postgres para persistir el usuario.

> **¿Por qué reiniciar el servidor después de cambiar el OpenAPI?** Porque el _validator_ lee la especificación al arrancar. Si modificas el archivo mientras `npm run dev` está corriendo, los cambios pueden no aplicarse hasta levantar el proceso de nuevo.

## ¿Qué pasa cuando una petición no cumple el contrato?

Aquí se ve el valor real del enfoque. Probando desde la documentación interactiva, si envías un `name` con una sola letra, la API responde `400 Bad Request` con un mensaje claro: el campo debe tener al menos dos caracteres.

Lo mismo ocurre con los otros campos:

- Si mandas `age` menor a 18, el _validator_ indica que el valor mínimo permitido es 18.
- Si el `email` no respeta el formato estándar, devuelve un error de formato.
- Si falta cualquier campo obligatorio, la petición se rechaza antes de llegar al _handler_.

Ninguna de esas validaciones vive en tu código de Express. Todas salen del contrato OpenAPI.

## ¿Qué ventajas trae validar desde OpenAPI?

Documentar y validar al mismo tiempo cambia la experiencia de quien consume tu API:

- Reduces código de validación repetitivo en cada endpoint.
- La documentación siempre coincide con el comportamiento real, porque es la misma fuente.
- Los errores son consistentes y descriptivos sin esfuerzo extra.
- Quien integra tu API sabe de antemano qué enviar y qué recibir.

> **¿Qué es un schema en OpenAPI?** Es la descripción estructurada de un objeto JSON: sus propiedades, tipos de dato, formatos y reglas como longitud mínima o valor mínimo. Funciona como contrato entre cliente y servidor.

Probar el endpoint desde la documentación generada también acelera el desarrollo. Refrescas la página, ves el bloque users con crear un nuevo usuario, ejecutas con datos válidos y obtienes el 201 con el ID del _timestamp_. Cambias un dato, fuerzas un error y el _validator_ responde sin que toques una línea de Express.