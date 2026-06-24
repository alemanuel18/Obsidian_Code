La gestión de reservas en aplicaciones web es un componente esencial para muchos negocios modernos. Implementar un sistema robusto que permita crear, consultar, actualizar y eliminar citas requiere una estructura organizada y un manejo adecuado de posibles conflictos. En este contenido, exploraremos cómo desarrollar un sistema de reservas utilizando Prisma como ORM y siguiendo buenas prácticas de arquitectura de software.

## ¿Cómo estructurar un controlador de reservas eficiente?

El controlador de reservas es el componente que maneja las solicitudes HTTP relacionadas con las citas o reservaciones. Para mantener un código limpio y mantenible, es recomendable seguir un patrón consistente para cada operación CRUD (Create, Read, Update, Delete).

Un controlador bien estructurado debe:

- Recibir y validar los parámetros de la solicitud
- Delegar la lógica de negocio a los servicios
- Manejar adecuadamente los errores
- Retornar respuestas con códigos HTTP apropiados

Para la actualización de reservas, el controlador debería verificar la existencia del recurso antes de intentar modificarlo:

```javascript
exports.updateReservation = async (req, res) => {
  try {
    const reservation = await reservationService.updateReservation(req.params.id, req.body);
    if (!reservation) {
      return res.status(404).json({ error: "Reserva no encontrada" });
    }
    return res.status(200).json(reservation);
  } catch (error) {
    return res.status(400).json({ error: error.message });
  }
};
```

De manera similar, para eliminar una reserva, es crucial verificar que el recurso exista:

```javascript
exports.deleteReservation = async (req, res) => {
  try {
    const reservation = await reservationService.deleteReservation(req.params.id);
    if (!reservation) {
      return res.status(404).json({ error: "Reserva no encontrada" });
    }
    return res.status(204).send();
  } catch (error) {
    return res.status(400).json({ error: error.message });
  }
};
```

## ¿Por qué separar la lógica en servicios?

**La separación de responsabilidades** es un principio fundamental en el desarrollo de software. Al mover la lógica de negocio a servicios dedicados, logramos:

- Mayor modularidad y reutilización de código
- Facilidad para realizar pruebas unitarias
- Mejor mantenibilidad a largo plazo
- Código más limpio y comprensible

Para implementar esta arquitectura, creamos un archivo `reservationService.js` dentro de la carpeta de servicios:

```javascript
const prisma = require('../path/to/prisma');

exports.createReservation = async (data) => {
  // Verificar si el horario ya está ocupado
  const conflict = await prisma.appointment.findFirst({
    where: {
      date: data.date,
      timeBlockId: data.timeBlockId
    }
  });

  if (conflict) {
    throw new Error("El horario ya está ocupado");
  }

  return prisma.appointment.create({
    data
  });
};
```

## ¿Cómo implementar la validación de conflictos en reservas?

Una de las partes más importantes de un sistema de reservas es **evitar conflictos de horarios**. No queremos que dos usuarios puedan reservar el mismo horario, lo que generaría problemas operativos.

Para implementar esta validación, debemos verificar si ya existe una reserva para la fecha y bloque de tiempo solicitados:

```javascript
exports.updateReservation = async (id, data) => {
  // Verificar si el nuevo horario ya está ocupado por otra reserva
  const conflict = await prisma.appointment.findFirst({
    where: {
      date: data.date,
      timeBlockId: data.timeBlockId,
      id: {
        not: parseInt(id, 10)
      }
    }
  });

  if (conflict) {
    throw new Error("El horario solicitado ya está ocupado");
  }

  return prisma.appointment.update({
    where: {
      id: parseInt(id, 10)
    },
    data
  });
};
```

Observa cómo en la validación para actualizar, excluimos la reserva actual del chequeo de conflictos usando `id: { not: parseInt(id, 10) }`. Esto permite que una reserva pueda actualizarse sin cambiar su horario sin generar un falso conflicto.

## ¿Cómo implementar operaciones de consulta y eliminación?

Las operaciones de consulta y eliminación son más sencillas, ya que no requieren validaciones complejas de conflictos:

```javascript
exports.getReservation = async (id) => {
  return prisma.appointment.findUnique({
    where: {
      id: parseInt(id, 10)
    }
  });
};

exports.deleteReservation = async (id) => {
  return prisma.appointment.delete({
    where: {
      id: parseInt(id, 10)
    }
  });
};
```

## ¿Cómo probar nuestro sistema de reservas?

Una vez implementado el sistema, es crucial probarlo para asegurar su correcto funcionamiento. Herramientas como **Postman** son ideales para probar APIs REST:

1. Importar la colección de endpoints en Postman
2. Configurar los headers de autenticación (usando tokens JWT)
3. Probar cada endpoint con diferentes escenarios

**Es importante verificar:**

- Que las validaciones de conflictos funcionen correctamente
- Que los códigos de estado HTTP sean apropiados
- Que la autenticación y autorización funcionen según lo esperado

Al probar el endpoint GET para obtener una reserva, debemos asegurarnos de incluir el token de autenticación en los headers:

```js
Authorization: Bearer [tu_token_jwt]
```

Si olvidamos incluir el token, recibiremos un error de acceso denegado: _"Access denied: No token provided"_.

La estructura de nuestro sistema nos permite detectar fácilmente errores. Por ejemplo, si olvidamos importar el servicio en el controlador, veremos un error como _"reservation service is not defined"_, lo que nos indica exactamente qué necesitamos corregir.

El desarrollo de un sistema de reservas robusto requiere atención a los detalles y una arquitectura bien pensada. La separación de responsabilidades entre controladores y servicios nos ayuda a mantener un código limpio y mantenible a largo plazo