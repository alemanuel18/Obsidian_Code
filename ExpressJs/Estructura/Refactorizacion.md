Separar la lógica de tu API en **controllers** y **services** es uno de los pasos más importantes cuando tu archivo `app.js` empieza a crecer sin control. Aquí vas a ver cómo refactorizar el registro y login de usuarios en una aplicación Node.js con Prisma, JWT y Bcrypt, manteniendo una arquitectura limpia y escalable.

## Por qué dividir controllers y services en una API Node.js

La idea central es simple: **los controllers manejan la lógica de la aplicación** (request, response, status codes) y **los services manejan la lógica del negocio** (crear usuarios, consultar base de datos, encriptar contraseñas). Cuando mezclas ambas en un solo archivo, mantener la app se vuelve un dolor de cabeza.

En la clase, todo lo que antes vivía dentro de `app.post` se reorganiza en dos capas. La capa que crea un usuario en la base de datos pertenece al _service_, mientras que la que recibe `req.body` y devuelve un `res.status(201)` pertenece al _controller_.

> **¿Qué diferencia hay entre un controller y un service?** El controller recibe la petición HTTP, valida estructura y responde al cliente. El service ejecuta la lógica de negocio: hashea contraseñas, consulta Prisma, genera tokens.

## Cómo construir el controller de register y login

El controller deja de usar `app.post` y se convierte en funciones exportables. Cada función es `async`, recibe `req`, `res` y un manejador de error, y envuelve la lógica en un `try/catch` para capturar fallos del service .

Para `register`, el flujo queda así:

- Extraer `email`, `password` y `name` desde `req.body`.
- Llamar con `await` a `registerUser(email, password, name)` del service.
- Retornar `res.status(201).json({ message: "User registered successfully" })`.
- Capturar errores con `res.status(400).json({ error: error.message })`.

Para `login`, el patrón es casi idéntico pero sin el `name`. La función espera un token desde `loginUser(email, password)` y lo devuelve en la respuesta. Aquí el detalle importante es que **solo retornas lo mínimo necesario**: el token JWT. Si tu admin lo requiere, también puedes incluir nombre, correo o avatar del usuario autenticado.

Al final del archivo, exportas ambas funciones con `module.exports = { register, login }` para usarlas en las rutas de autenticación.

## Cómo importar el service desde el controller

Dentro del controller, importas las funciones del service con `require` apuntando a la carpeta `services/AuthService.js`. Esta separación es la que permite que cuando algo falle en producción, sepas exactamente dónde buscar: si es un problema de respuesta HTTP, está en el controller; si es un problema con Prisma o Bcrypt, está en el service.

## Cómo implementar el AuthService con Prisma, Bcrypt y JWT

El archivo `AuthService.js` concentra toda la lógica pesada. Aquí viven los imports de **Bcrypt** para hashear contraseñas, **JSON Web Token** para generar tokens y **Prisma** para hablar con la base de datos .

La función `registerUser` ejecuta tres pasos clave:

1. Hashear la contraseña con `await bcrypt.hash(password, 10)`.
2. Crear el usuario con `prisma.user.create` pasando `data` con email, name, el password hasheado y el rol por defecto en `"user"`.
3. Retornar el `newUser` resultante.

Un detalle que rompe la primera ejecución: al pasar los datos a Prisma, debes usar la clave `password` con el valor hasheado, no `hashedPassword`. Si nombras mal la propiedad, Prisma responde con _Password is missing_ porque no encuentra el campo en el modelo.

> **¿Por qué se usa el valor 10 en bcrypt.hash?** Es el número de _salt rounds_: define cuántas veces se aplica el algoritmo de hashing. A más rondas, más seguro pero más lento.

## Cómo validar el login y generar el token JWT

La función `loginUser` sigue una secuencia de validación que protege contra ataques de enumeración:

- Buscar el usuario con `prisma.user.findUnique({ where: { email } })`.
- Si no existe, lanzar `throw new Error("invalid email or password")`.
- Comparar contraseñas con `await bcrypt.compare(password, user.password)`.
- Si no coinciden, lanzar el mismo error genérico.

El mensaje **"invalid email or password"** es intencional: no le das pistas a un atacante sobre si el correo existe o si solo falló la contraseña. Es una práctica básica de seguridad que se respeta sin importar qué validación falle.

Después de validar, generas el token con `jwt.sign({ id: user.id, rol: user.rol }, process.env.JWT_SECRET, { expiresIn: "4h" })`. Las cuatro horas de expiración son un balance entre experiencia de usuario y seguridad: lo suficientemente largo para no pedir login constante, lo suficientemente corto para limitar el daño si el token se compromete.

## Cómo organizar la estructura final del proyecto

La app termina con esta estructura dentro de `src`: `controllers`, `middlewares`, `routes`, `services`, `utils`, más los archivos `app.js` y `server.js` . El `app.js` configura Express y los middlewares; el `server.js` solo arranca el servidor en el puerto definido.

Dos ajustes prácticos que aparecen al mover archivos:

- Actualizar los scripts en `package.json`: `"dev"` apunta a `src/server.js` y `"start"` también.
- Agregar `module.exports = app` al final de `app.js`, porque sin esa exportación el `server.js` no puede arrancar la aplicación.

Las rutas también cambian de prefijo. Dentro de `app.js` se monta el router principal bajo `/api`, lo que permite versionar la API más adelante (`/api/v1`, `/api/v2`) sin romper clientes existentes. El endpoint final para registrar queda en `POST /api/auth/register` y para autenticar en `POST /api/auth/login`.

## Errores comunes al refactorizar y cómo resolverlos

Durante la prueba en Postman aparecen dos fallos típicos:

- **Password is missing**: ocurre por nombrar mal la propiedad al pasar datos a Prisma. Solución: usar `password: hashedPassword` en el objeto `data`.
- **secretOrPrivateKey must have a value**: típico _typo_ en la variable de entorno. Si tu `.env` tiene `JWT_SECRET` pero el código lee `JTW_SECRET`, JWT no encuentra la llave y truena. Revisa siempre la coincidencia exacta entre `.env` y `process.env`.

Una vez resueltos, `POST /api/auth/register` responde con _User registered successfully_ y `POST /api/auth/login` devuelve un token JWT válido listo para usarse en rutas protegidas.