La gestión de permisos y roles es un componente fundamental en el desarrollo de aplicaciones web modernas. En este contenido, exploraremos cómo implementar un sistema de administración para una aplicación de reserva de citas, donde solo los usuarios con rol de administrador pueden crear bloques de tiempo disponibles para las citas. Esta estructura no solo mejora la seguridad de nuestra aplicación, sino que también establece un flujo de trabajo organizado y eficiente.

## ¿Cómo estructurar la lógica de administración en una API de reservas?

Antes de sumergirnos en el código, es importante entender la lógica de negocio detrás de nuestra aplicación. **Solo un administrador puede agregar bloques de tiempo** en los que los usuarios pueden registrar sus citas. Esta restricción requiere implementar una estructura de control de acceso basada en roles.

Para lograr esto, necesitamos crear:

1. Rutas específicas para administradores
2. Controladores que manejen las solicitudes
3. Servicios que implementen la lógica de negocio
4. Validaciones de permisos basadas en roles

## Configuración de las rutas de administrador

El primer paso es establecer las rutas que solo serán accesibles para los administradores. Comenzamos modificando nuestro archivo de rutas principal:

```javascript
// routes/index.js
router.use('/admin', adminRoutes);

const adminRouter = require('./admin');
```

Luego, creamos un archivo específico para las rutas de administración:

```javascript
// routes/admin.js
const router = require('express').Router();
const adminController = require('../controllers/adminController');

// Ruta para crear bloques de tiempo
router.post('/timeblocks', adminController.createTimeBlock);

// Ruta para listar todas las reservaciones
router.get('/reservations', adminController.listReservations);

module.exports = router;
```

Estas rutas definen dos funcionalidades principales para los administradores:

- Crear nuevos bloques de tiempo disponibles para citas
- Ver todas las reservaciones realizadas por los usuarios

## Implementación del controlador de administración

El controlador es responsable de recibir las solicitudes HTTP, validar los permisos del usuario y coordinar con los servicios correspondientes:

```javascript
// controllers/adminController.js
const createTimeBlockService = require('../services/adminService').createTimeBlockService;
const listReservationsService = require('../services/adminService').listReservationsService;

const createTimeBlock = async (req, res) => {
  // Verificar si el usuario tiene rol de administrador
  if (req.user.role !== 'admin') {
    return res.status(403).json({ error: 'Access Denied' });
  }

  // Obtener datos del cuerpo de la solicitud
  const { startTime, endTime } = req.body;

  try {
    // Llamar al servicio para crear el bloque de tiempo
    const newTimeBlock = await createTimeBlockService(startTime, endTime);
    res.status(201).json(newTimeBlock);
  } catch (error) {
    res.status(500).json({ error: 'Error creating time block' });
  }
};

const listReservations = async (req, res) => {
  // Verificar si el usuario tiene rol de administrador
  if (req.user.role !== 'admin') {
    return res.status(403).json({ error: 'Access Denied' });
  }

  try {
    // Obtener todas las reservaciones
    const reservations = await listReservationsService();
    res.json(reservations);
  } catch (error) {
    res.status(500).json({ error: 'Error obteniendo las reservaciones' });
  }
};

module.exports = {
  createTimeBlock,
  listReservations
};
```

## Validación de permisos de administrador

**Un aspecto crucial de nuestra implementación es la validación de permisos**. Observa cómo en cada función del controlador verificamos si el usuario tiene el rol de administrador:

```javascript
if (req.user.role !== 'admin') {
  return res.status(403).json({ error: 'Access Denied' });
}
```

Esta simple verificación garantiza que solo los usuarios con el rol adecuado puedan acceder a estas funcionalidades. Si un usuario sin permisos intenta acceder, recibirá un error 403 (Forbidden).

## ¿Qué información necesitamos para crear bloques de tiempo?

Para crear un bloque de tiempo, necesitamos dos piezas esenciales de información:

1. **startTime**: La hora de inicio del bloque
2. **endTime**: La hora de finalización del bloque

Estos datos se extraen del cuerpo de la solicitud:

```javascript
const { startTime, endTime } = req.body;
```

Luego, estos valores se pasan al servicio correspondiente, que se encargará de la lógica de negocio y la interacción con la base de datos.

## Estructura de servicios para la lógica de negocio

Aunque no se muestra la implementación completa de los servicios en el código proporcionado, es importante entender que estos serán responsables de:

1. Validar los datos recibidos
2. Interactuar con la base de datos (probablemente usando Prisma, según se menciona)
3. Manejar cualquier lógica de negocio específica
4. Devolver los resultados al controlador

Esta separación de responsabilidades sigue el principio de responsabilidad única y hace que nuestro código sea más mantenible y testeable.

## ¿Por qué es importante la separación de responsabilidades?

La estructura que estamos implementando sigue un patrón común en el desarrollo de aplicaciones:

- **Rutas**: Definen los puntos de entrada a nuestra API
- **Controladores**: Manejan las solicitudes HTTP y coordinan con los servicios
- **Servicios**: Implementan la lógica de negocio y la interacción con la base de datos

**Esta separación ofrece múltiples beneficios**:

1. **Mantenibilidad**: Cada componente tiene una responsabilidad clara
2. **Testabilidad**: Es más fácil escribir pruebas unitarias para componentes aislados
3. **Escalabilidad**: Podemos modificar o extender un componente sin afectar a los demás
4. **Legibilidad**: El código es más fácil de entender y seguir

La implementación de esta estructura puede parecer más trabajo inicialmente, pero a largo plazo facilita enormemente el mantenimiento y la evolución de la aplicación.