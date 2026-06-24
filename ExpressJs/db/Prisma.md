Conectar **Prisma ORM con PostgreSQL** te permite administrar tu base de datos desde una aplicación Node.js de forma programática, segura y escalable. Aquí aprendes a instalar Prisma, configurar el esquema, ejecutar migraciones y listar usuarios desde una API en Express.

## Qué es Prisma y por qué usarlo con PostgreSQL

Prisma es un _ORM_ (Object Relational Mapper) que traduce tu código JavaScript en consultas SQL. En lugar de escribir queries a mano, defines modelos en un archivo de esquema y Prisma se encarga del resto: conexión, validación de tipos y migraciones.

La idea es simple: tú describes cómo se ve un usuario en tu app y Prisma sincroniza esa estructura con tu base de datos PostgreSQL.

> **¿Qué es un ORM?** Es una capa que conecta tu aplicación con la base de datos usando objetos en vez de SQL puro. Te ahorra escribir queries y reduce errores de sintaxis.

## Qué paquetes necesito instalar para usar Prisma

Desde la terminal del proyecto, instala las dependencias en este orden :

- `npm install prisma --save-dev` para el CLI de Prisma como dependencia de desarrollo.
- `npm install @prisma/client` para el cliente que usarás dentro del código.
- `npm install pg` como driver oficial de PostgreSQL.

Con estos tres paquetes ya tienes lo necesario para inicializar el proyecto.

## Cómo inicializar Prisma en un proyecto Node.js

Ejecuta el comando `npx prisma init` . Esto crea dos cosas clave: la carpeta `prisma` con el archivo `schema.prisma` y un archivo `.env` donde vivirá tu cadena de conexión.

El archivo `schema.prisma` es el corazón de tu configuración. Ahí defines el _datasource_ (qué base de datos usas), el _generator_ (qué cliente generar) y los _models_ (la forma de tus tablas).

Un tip práctico: instala la extensión oficial de Prisma en tu editor. Te da resaltado de sintaxis y autocompletado, lo que vuelve mucho más legible el archivo de esquema.

## Cómo defino el modelo de usuario en schema.prisma

El modelo de usuario sigue una estructura programática donde cada campo tiene un tipo explícito:

- `id` como entero autoincremental y llave primaria.
- `name` como _string_ obligatorio.
- `email` como _string_ único para evitar duplicados.

Este enfoque previene fallas comunes que aparecían cuando escribías SQL a mano, como permitir emails repetidos o tipos inconsistentes.

## Cómo configuro la cadena de conexión a PostgreSQL

En el archivo `.env` actualiza la variable `DATABASE_URL` con tus credenciales reales . La estructura es:

`postgresql://USUARIO:PASSWORD@localhost:5432/postgres`

Reemplaza `USUARIO` por el usuario que creaste en Postgres, `PASSWORD` por tu contraseña, y deja `localhost:5432` si trabajas en local. El `5432` es el puerto por defecto de PostgreSQL.

Más adelante, cuando muevas la app a producción, solo cambias este string por uno que apunte a una base de datos en la nube.

## Cómo genero el cliente de Prisma y ejecuto migraciones

Después de definir el modelo, corre `npx prisma generate` . Este comando crea el cliente tipado que vas a importar en tu código.

Luego ejecuta la migración inicial con `npx prisma migrate dev --name init` . Aquí pasan dos cosas importantes:

- Prisma lee tu `schema.prisma` y genera archivos SQL dentro de `prisma/migrations`.
- Aplica esos cambios a tu base de datos PostgreSQL, creando las tablas reales.

> **¿Qué hace prisma migrate dev?** Sincroniza tu esquema con la base de datos y guarda un historial de cambios versionados. Lo usas en desarrollo para iterar rápido.

## Cómo conecto Prisma Client con Express

En tu archivo `app.js` importas el cliente y creas una instancia única:

```js 
const { PrismaClient } = require('@prisma/client'); 
const prisma = new PrismaClient();
```

Esta instancia ya sabe leer la `DATABASE_URL` desde tus variables de entorno automáticamente, sin configuración extra.

## Cómo listo usuarios desde la base de datos con Prisma

Ahora creas un endpoint `GET /db-users` que consulte la tabla. Como las operaciones de base de datos son asíncronas, la función debe ser `async` y usar `try/catch` para manejar errores :

```js 
app.get('/db-users', async (req, res) => { 
	try { 
	const users = await prisma.user.findMany(); 
	res.json(users); 
	} catch (error) { 
	res.status(500).json({ error: 'Error al comunicarse con la base de datos' }); 
	} 
});
```

El método `findMany()` trae todos los registros de la tabla `user`. Prisma expone también `findUnique`, `create`, `update` y `delete`, cubriendo el CRUD completo.

## Por qué uso async await y try catch en este endpoint

La consulta a Postgres tarda milisegundos pero no es instantánea. Sin `await`, tu respuesta saldría antes de tener los datos. Y sin `try/catch`, cualquier fallo de conexión rompería el servidor entero.

El `status 500` indica un error del lado del servidor, lo que ayuda al frontend a distinguir entre un problema de red y una respuesta válida vacía.

## Cómo verifico que la conexión funciona correctamente

Levanta el servidor con `npm run dev` y visita `http://localhost:PUERTO/db-users` en el navegador. Si ves un array vacío `[]`, la conexión funciona pero aún no hay registros.

Si vieras el mensaje de error, revisa tres cosas:

- La cadena `DATABASE_URL` con usuario y contraseña correctos.
- Que el servicio de PostgreSQL esté corriendo en tu máquina.
- Que la migración se haya aplicado sin errores.

El siguiente paso natural es insertar usuarios usando `prisma.user.create()`. ¿Cómo crees que estructurarías ese endpoint? 