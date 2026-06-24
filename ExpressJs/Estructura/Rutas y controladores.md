Construir un módulo de reservaciones en una API REST con Node.js y Express requiere definir rutas claras, controladores bien organizados y servicios que conecten con la base de datos. Aprenderás a estructurar los puntos de entrada para crear, obtener, actualizar y eliminar citas, aplicando autenticación con middleware y siguiendo buenas prácticas de modularidad.

## Cómo se definen las rutas del módulo de reservations

Todo arranca en el archivo principal de rutas. Ahí declaras una constante `reservations` que importa el archivo del recurso y se conecta al router con `router.use`, igual que hicimos con el módulo de administración.

Dentro del nuevo archivo `reservations.js` traes los elementos que ya venías usando, pero con un detalle importante: los controllers que importas no son los de admin, sino los de este recurso. Por eso debes crear un `reservationController` propio dentro de la carpeta de controllers.

> **¿Qué hace router.use en Express?** Conecta un prefijo de ruta con un archivo de rutas específico. Así, todas las peticiones que entren a `/reservations` se manejan en el archivo dedicado a ese recurso.

## Cuáles son los cuatro puntos de entrada que necesitas

Cada operación tiene su verbo HTTP y su middleware de autenticación. La estructura queda así:

- `router.post('/', authenticateToken, reservationController.createReservation)` para crear una nueva reserva.
- `router.get('/:id', authenticateToken, reservationController.getReservation)` para obtener el detalle de una cita por su ID.
- `router.put('/:id', authenticateToken, reservationController.updateReservation)` para actualizar la reserva con el cuerpo completo.
- `router.delete('/:id', authenticateToken, reservationController.deleteReservation)` para eliminarla.

No olvides cerrar el archivo con `module.exports = router`, porque sin esa exportación el archivo principal no podrá usar las rutas que acabas de definir.

## Cómo se construye el reservationController paso a paso

El controller centraliza la lógica de cada operación. En lugar de exportar funciones una por una al final del archivo, puedes usar `exports.nombreFuncion` directamente, lo que hace el código más limpio y fácil de mantener.

La primera función es `createReservation`. Recibe `req` y `res`, envuelve la lógica en un bloque `try/catch` y llama a `reservationService.createReservation` pasándole `req.body` completo. Si todo sale bien, responde con un `res.status(201).json(reservation)`. Si algo falla, devuelve un `res.status(400)` con `error.message`.

```javascript 
exports.createReservation = async (req, res) => { 
	try { 
		const reservation = await reservationService.createReservation(req.body);
		res.status(201).json(reservation); 
	} catch (error) { 
		res.status(400).json({ error:
		error.message }); 
	} 
};
```

## Por qué validar la existencia de la reservation antes de responder

En `getReservation` no basta con consultar la base de datos. Tienes que validar que el resultado realmente exista, porque alguien puede enviar un ID que no está registrado.

Si `reservation` viene vacío, debes hacer un `return` con `res.status(404).json({ error: 'reservation not found' })`. De lo contrario, tu API respondería con datos vacíos y el cliente no sabría qué pasó.

> **¿Qué código HTTP usar cuando un recurso no existe?** El 404. Indica que el servidor entendió la petición pero no encontró el recurso solicitado. Es distinto del 400, que se usa para errores en la solicitud del cliente.

Cuando la reservation sí existe, respondes con `res.json(reservation)` y listo. El manejo de errores genéricos sigue cayendo en un `res.status(400)` con el mensaje correspondiente.

## Qué diferencia hay entre update y delete en una API REST

Ambas operaciones reciben un ID por parámetros, pero su comportamiento cambia según lo que necesite la base de datos.

- **updateReservation** demanda el cuerpo completo de la petición. El usuario envía los datos modificados en `req.body` y tú los pasas al servicio junto con el ID.
- **deleteReservation** solo necesita el ID. No hay cuerpo, no hay payload extra: el servicio elimina el registro y devuelve una confirmación.

Esa diferencia explica por qué en las rutas el `put` y el `delete` apuntan al mismo patrón `/:id`, pero internamente la lógica del controller no es la misma.

## Cómo se conecta el controller con el reservationService

El controller nunca toca la base de datos directamente. Su trabajo es recibir la petición, validar lo mínimo y delegar la operación al `reservationService`, que es quien sabe cómo guardar, leer, actualizar o borrar.

Esta separación tiene un beneficio claro: si mañana cambias de base de datos o de ORM, solo modificas el servicio. Las rutas y los controllers se quedan intactos, y eso protege tu API de reescrituras innecesarias.

Ahora te toca a ti: implementa `updateReservation` y `deleteReservation` siguiendo la misma lógica. Recuerda que update recibe el cuerpo completo y delete solo el ID. Comparte tu resultado en los comentarios y nos vemos en la siguiente clase para seguir construyendo el módulo.