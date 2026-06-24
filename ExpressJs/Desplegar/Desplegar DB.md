Desplegar una API de Express con base de datos en la nube deja de ser un dolor de cabeza cuando usas Railway junto con Prisma. Aquí verás cómo llevar tu MVP de autenticación y permisos a un entorno productivo, conectar PostgreSQL remoto y validar que todo funcione antes de abrir la puerta a usuarios reales.

Esto es relevante si ya construiste un _CRUD_ con Express, manejas tokens y necesitas dar el siguiente paso: tener tu API viva en internet sin pelearte con servidores.

## ¿Qué incluye el MVP antes de desplegar la API?

Antes de mover nada a la nube, conviene saber qué tienes en las manos. El producto mínimo viable que se construyó a lo largo del curso ya cubre lo esencial para considerarse funcional .

- Autenticación de usuarios con registro previo.
- Generación de _token_ con permisos asociados.
- Endpoints diferenciados para usuario y administrador.
- Conexión activa con base de datos vía Prisma.

> **¿Qué es un MVP en el contexto de una API?** Es la versión más simple de tu API que ya permite registrar usuarios, autenticarlos y exponer endpoints protegidos. No tiene todas las funciones, pero sí las suficientes para probar la idea.

Faltan características, claro. Por eso el instructor entrega un RFC (_request for comments_) con las particularidades que debes construir para que la API quede totalmente disponible .

## ¿Por qué usar Railway para desplegar tu API?

Railway es un servicio de terceros que simplifica el despliegue de aplicaciones y bases de datos en minutos . Tú delegas la infraestructura y te enfocas en el código.

La plataforma ofrece un _free trial_ para empezar a experimentar sin pagar. Y según la experiencia compartida, aplicaciones reales con usuarios en producción no superan los **cinco dólares mensuales** de uso .

## ¿Cómo crear el proyecto y la base de datos en Railway?

Desde el dashboard, el flujo es directo:

1. Crear un nuevo proyecto.
2. Elegir el origen: repositorio de GitHub, _template_ o base de datos PostgreSQL.
3. Seleccionar PostgreSQL para que Railway despliegue el servicio automáticamente.
4. Esperar a que termine el aprovisionamiento.

Con un solo clic ya tienes el servicio corriendo y listo para conectarse .

## ¿Dónde está la URL de conexión a la base de datos?

En la pestaña **Connect** del servicio, Railway muestra varias opciones. La que importa es el _connection URL_, que reúne usuario, contraseña, host, puerto y nombre de la base de datos inicial .

Es el mismo formato que usabas en local, pero en lugar de _localhost_ tienes una URL asignada por Railway.

## ¿Cómo conectar Prisma con la base de datos en la nube?

Copia el _connection URL_ y pégalo en tu archivo `.env` como valor de `DATABASE_URL`. Comenta la conexión local previa para conservarla como respaldo .

> **¿Por qué debo agregar el archivo .env al gitignore?** Porque contiene la contraseña real de tu base de datos. Aunque tu repositorio sea privado, exponer credenciales permite que cualquiera con acceso al código se conecte a tus datos sensibles.

Con la variable lista, ejecuta los comandos de Prisma desde la terminal para sincronizar el esquema:

- `npx prisma migrate deploy` aplica las migraciones existentes y valida la conexión .
- `npx prisma generate` regenera el cliente para reflejar cualquier cambio .
- `npx prisma db pull` confirma que los modelos se reconocen correctamente en la nueva base .

Si alguno falla, lo más probable es que tu _connection URL_ tenga un error. Revísala antes de seguir.

## ¿Cómo poblar la base de datos con datos semilla?

Ejecuta el script semilla que se proporciona en recursos con `node prisma/seed.js` apuntando a la carpeta correspondiente . El proceso construye usuarios y elementos clave para que la API tenga información inicial con la que trabajar.

Cuando la terminal devuelve el _prompt_, los datos ya están guardados en Railway. Puedes validarlo desde la interfaz visual del servicio: ahí aparecen las tablas `appointments`, `users` y el _admin user_ recién creado .

## ¿Cómo validar que la API funciona contra la base de datos remota?

Levanta el servidor en local con `npm run dev`. El servicio queda disponible en el puerto **3005** . Aunque el código corre en tu máquina, las consultas viajan a Railway.

Desde Postman, prueba el endpoint de registro con un usuario nuevo. Notarás que la respuesta tarda un poco más que antes, y eso es buena señal: significa que la petición está llegando hasta la base de datos en la nube .

## ¿Cómo confirmar que el usuario se guardó correctamente?

Vuelve al panel de Railway y actualiza la tabla `users`. Ahí verás el registro recién creado con su `password hash` ya encriptado . Si necesitas modificar algún campo, como otorgar permisos de _admin_, puedes editarlo directamente desde la interfaz web.

Después prueba el _login_ con ese usuario. Si recibes el _token_ de vuelta, la autenticación está funcionando contra la base remota y tu API está, del lado de los datos, oficialmente desplegada .

## ¿Qué es un RFC y para qué sirve en este proyecto?

Un RFC (_request for comments_) es un documento que describe qué cambios proponer, cómo implementarlos y qué impacto tienen . Se usa para proponer cambios de arquitectura o nuevos _features_ antes de tocar código.

En el material del curso encontrarás un RFC con todas las posibilidades para que esta implementación de citas médicas funcione completa: gestión de pacientes, registro de médicos, agenda y más. Ya sabes trabajar un _CRUD_ y conectarte a una base de datos, así que el siguiente paso es proponer mejoras.