Crear un **admin service en Node.js con Prisma** te permite gestionar bloques de disponibilidad y listar reservaciones de forma segura. Aquí aprenderás a estructurar la lógica administrativa, proteger rutas con autenticación por token y validar roles para que solo un _admin_ pueda acceder.

## Cómo se estructura el admin service con Prisma

La idea es centralizar en un solo archivo la comunicación con la base de datos para las operaciones administrativas. Nada de mezclar responsabilidades.

Dentro de `service/` creas `adminService.js` e importas Prisma como en los demás recursos. No necesitas _JSON Web Token_ aquí porque la validación del token vive en el middleware, no en el service.

> **¿Qué hace un service en una API REST?** Concentra la lógica de negocio y el acceso a la base de datos, separándola del controller. Así tu código queda más limpio y fácil de mantener.

Desde el inicio del flujo administrativo se plantea esta separación de capas, donde el service se conecta con Prisma y expone funciones que luego consume el controller.

## Cómo crear un bloque de tiempo con prisma.timeBlock.create

El primer servicio es `createTimeBlockService`, una función `async` que recibe `startTime` y `endTime`. Su trabajo es insertar un nuevo bloque de disponibilidad para que los usuarios lo reserven.

La implementación queda así:

```javascript 
const createTimeBlockService = async (startTime, endTime) => { 
	const newTimeBlock = await prisma.timeBlock.create({ data: 
		{ startTime: new Date(startTime), 
		endTime: new Date(endTime), 
	}, 
}); 
return newTimeBlock; };
```

Fíjate en el uso de `new Date()` para convertir los valores recibidos en objetos de fecha válidos. Es un detalle pequeño pero clave para que Prisma los almacene correctamente.

## Cómo listar reservaciones con findMany e include

El segundo servicio es `listReservationService`. No recibe parámetros y devuelve todas las citas con la información del usuario y del bloque asociado.

```javascript 
const listReservationService = async () => { 
	const reservations = await prisma.appointments.findMany({ include: 
		{ user: true, timeBlock: true, 
	},
}); 
return reservations; };
```

El `include` con `user: true` y `timeBlock: true` es lo que enriquece la respuesta. En lugar de devolver solo IDs, te trae el objeto completo del usuario y del bloque. Mucho más útil para una vista administrativa.

Al final exportas ambos servicios con `module.exports` para que el controller pueda usarlos.

## Por qué proteger la ruta con authenticate-token y rol admin

Al probar el endpoint en Postman aparece un error: el controller intenta leer el rol del usuario, pero el usuario no llega. ¿La razón? Falta el middleware de autenticación.

> **¿Por qué necesito un middleware de autenticación antes de validar el rol?** Porque el middleware decodifica el token y adjunta el usuario al request. Sin ese paso, no hay forma de saber qué rol tiene quien hace la petición.

La corrección es importar el middleware desde la carpeta de _middlewares_ y aplicarlo antes de la validación de rol:

```javascript 
const authenticateToken = require('../middlewares/authorization');
```

Ahora la ruta exige dos cosas: un token válido y un rol de _admin_. Esa doble capa es la que mantiene la API segura.

## Cómo se comportan los errores según el token enviado

Probar los escenarios negativos es tan importante como probar el camino feliz. En Postman se validan tres casos concretos:

- Token válido de un usuario admin: devuelve el listado completo de reservaciones con datos de usuario y bloque.
- Token inválido o manipulado: la API responde _invalid token_.
- Token válido pero de un usuario sin rol admin: la respuesta es _acceso denegado_.

Para probar el tercer caso se registra un usuario nuevo con un correo distinto, se hace login, se copia el token y se intenta listar reservaciones. El sistema bloquea la operación, justo como debe ser.

## Cómo interpretar un 404 al crear un bloque de tiempo

Al probar el endpoint para crear un bloque aparece un _404 not found_. La ruta llamada era `admin/timeBlock`, pero el endpoint real es `admin/timeBlocks` en plural.

> **¿Qué significa un 404 en una API?** Que la ruta solicitada no existe en el servidor. Casi siempre es un error de tipeo en la URL o un endpoint mal definido en el router.

Entender los códigos HTTP te ahorra horas de depuración. Un 401 te habla de autenticación, un 403 de permisos, un 404 de rutas. Cada error es una pista.

Una vez corregida la URL, la petición devuelve el bloque creado con su ID, listo para que los usuarios lo elijan al reservar.

##  clave que aparecen en la implementación

Varias piezas técnicas se conectan en este flujo y vale la pena identificarlas:

- _Prisma Client_ como ORM para consultas tipadas a la base de datos .
- `prisma.timeBlock.create` para insertar registros con conversión de fechas .
- `prisma.appointments.findMany` con `include` para traer relaciones .
- `module.exports` para exponer los servicios al controller .
- Middleware `authenticateToken` para proteger rutas .
- Validación de rol admin para autorizar operaciones sensibles .
- Pruebas en Postman con tokens válidos, inválidos y sin permisos .
- Interpretación de códigos HTTP como 400, 401, 403 y 404 .