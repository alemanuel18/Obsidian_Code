Construir un endpoint que devuelva el historial de citas de un usuario autenticado requiere combinar rutas, controladores, servicios y middleware de autenticación. Esta guía muestra cómo implementar ese punto de entrada en una API con Express y Prisma, asegurando que solo quien tiene un token válido pueda consultar su información.

## ¿Cómo se estructura la ruta para listar citas por usuario?

El primer paso ocurre en el archivo `routes/index`, donde se registra el recurso anidado que conecta usuarios con sus citas. La idea es que cada usuario pueda acceder únicamente a sus propios _appointments_, así que la ruta se construye sobre el identificador del usuario.

Dentro del archivo se importa el módulo de citas y se monta con `router.use`, apuntando al recurso `users` y delegando la lógica a `appointments` .

```js 
const appointments = require('./appointments'); router.use('/users', appointments);
```

Luego, en `routes/appointments.js`, se define la lógica con Express. Aquí entra en juego `router.get`, que recibe el ID del usuario como parámetro dinámico y dispara el controlador correspondiente.

> **¿Por qué proteger el endpoint con autenticación?** Porque las citas son información sensible. Sin un _middleware_ como `authenticateToken`, cualquiera podría leer el historial ajeno con solo conocer un ID.

El _middleware_ `authenticateToken` se importa desde la carpeta de _middlewares_ y se coloca antes del controlador en la definición de la ruta . Solo pasa quien tenga un token válido emitido en el _login_.

## ¿Qué hace el controlador appointmentController?

El controlador actúa como puente entre la petición HTTP y la lógica de negocio. No consulta la base de datos directamente, sino que delega esa responsabilidad al servicio.

En `controllers/appointmentController.js` se define `getUserAppointments` como una función `async` que recibe `req` y `res`. La estructura básica incluye un bloque `try/catch` para manejar errores con elegancia.

- Extrae el `userId` desde `req.params.id`.
- Llama a `appointmentService.getUserAppointments(userId)`.
- Devuelve las citas en formato JSON cuando todo sale bien.
- Responde con `status 500` y un mensaje claro si algo falla.

```js 
exports.getUserAppointments = async (req, res) => { 
	try { 
		const userId = req.params.id; const appointments = await
		appointmentService.getUserAppointments(userId); res.json(appointments); 
	} catch (error) { 
		res.status(500).json({ 
			error: 'Error al obtener el historial de citas' 
		}); 
	} 
};
```

Esta separación entre controlador y servicio mantiene el código mantenible. Si mañana cambias de Prisma a otro ORM, solo modificas el servicio.

## ¿Cómo consulta Prisma las citas en el servicio?

El servicio es donde vive la conversación real con la base de datos. En `services/appointmentService.js` se importa la instancia de Prisma y se define la función que ejecuta la consulta.

La magia ocurre con `prisma.appointment.findMany`, que recibe un objeto `where` para filtrar por `userId` y un `include` para traer también el `timeBlock` asociado .

```js 
exports.getUserAppointments = async (userId) => { 
	try { 
		const appointments = await prisma.appointment.findMany({ 
			where: { 
				userId: parseInt(userId) 
			}, 
			include: { timeBlock: true } 
		}); 
		return appointments; 
	} catch (error) { 
		throw new Error('Error al obtener el historial de citas'); 
	} 
};
```

Fíjate en `parseInt(userId)`. Los parámetros de URL llegan como _string_, pero Prisma espera un entero cuando el campo está tipado así en el esquema. Saltarte esa conversión genera errores silenciosos que cuestan horas de depuración.

> **¿Para qué sirve el include en Prisma?** Para traer datos relacionados en una sola consulta. Aquí trae el bloque de tiempo de cada cita, evitando llamadas adicionales a la base de datos.

## ¿Cómo probar el endpoint con Postman?

Una vez que el código está guardado, llega el momento de validar que todo conecta. Postman es la herramienta ideal para enviar peticiones autenticadas y revisar la respuesta.

### Los pasos para la prueba son directos:

1. Importar la colección de la API desde los recursos del curso.
2. Copiar el token JWT de la última autenticación realizada.
3. Pegarlo en el apartado de autorización de la petición.
4. Indicar el ID del usuario, por ejemplo `1`, en la URL.
5. Levantar el servidor con `npm run dev` antes de enviar.

Al ejecutar la petición, la respuesta debe incluir la lista de citas asociadas a ese usuario junto con el `timeBlock` correspondiente. Si solo hay una cita registrada, verás un _array_ con un único objeto, lo que confirma que el filtro `where` está operando bien.