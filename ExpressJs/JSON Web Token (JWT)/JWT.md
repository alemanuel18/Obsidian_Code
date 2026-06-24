La autenticación con JSON Web Token (JWT) te permite proteger rutas en tu aplicación Node.js para que solo usuarios autorizados accedan a ciertos recursos. Aquí aprendes a configurar un _middleware_ que valide tokens y rechace solicitudes no autorizadas, paso a paso, con los paquetes adecuados.

## Qué paquetes necesitas para trabajar con JWT y encriptación

Antes de escribir lógica, instala las dos librerías que sostienen toda la autenticación.

- `jsonwebtoken`: genera y verifica los tokens que identifican a cada usuario. Lo instalas con `npm install jsonwebtoken`.
- `bcryptjs`: encripta contraseñas antes de guardarlas, para que nunca queden en texto plano. Lo instalas con `npm install bcryptjs`.

Con estos dos paquetes ya tienes la base para construir un sistema de autenticación serio.

> **¿Qué es un JSON Web Token?** Es una cadena firmada que identifica a un usuario autenticado. El servidor la genera al iniciar sesión y el cliente la envía en cada solicitud para acceder a rutas protegidas.

## Cómo crear el middleware de autenticación en auth.js

Dentro de la carpeta `middlewares` creas un archivo `auth.js`. Ese archivo concentra toda la lógica de validación del token.

Empiezas importando la librería con `const jwt = require('jsonwebtoken')`. Luego defines una función llamada `authenticateToken` que recibe `req`, `res` y `next`. El parámetro `next` es clave: cuando la validación es exitosa, le indica a Express que continúe con la siguiente función de la cadena.

## Cómo extraer el token del header de Authorization

Las solicitudes autenticadas mandan el token en el encabezado `Authorization` con el formato `Bearer <token>`. Por eso necesitas separar ese string para quedarte solo con el token.

js const token = req.header('Authorization').split(' ')[1];

El `split(' ')` divide la cadena en dos partes y la posición `[1]` te da el token puro, sin la palabra `Bearer`.

## Cómo manejar la ausencia de token con un error 401

Si el cliente no envía ningún token, debes cortar la solicitud con un código `401 Unauthorized`. Esto comunica de forma clara que el acceso fue denegado por falta de credenciales.

```js 
if (!token) { 
	return res.status(401).json({ 
		error: 'Access denied: No token provided' 
	}); 
}
```

La diferencia entre **401 y 403** es importante: 401 significa que no enviaste credenciales, 403 que sí las enviaste pero no son válidas.

## Cómo verificar el token con jwt.verify y variables de entorno

La verificación del token usa `jwt.verify`, que recibe el token, el secreto y un _callback_ con el error y el usuario decodificado. El secreto nunca debe vivir en el código fuente.

Lo defines en tu archivo de variables de entorno como `JWT_SECRET=Platzi` (o cualquier frase que tú elijas) y lo lees con `process.env.JWT_SECRET`. Mantenerlo fuera del repositorio evita que cualquiera firme tokens válidos.

```js 
jwt.verify(token, process.env.JWT_SECRET, (err, user) => { 
	if (err) return res.status(403).json({ 
		status: 'error', error: 'Invalid token' 
	}); 
	req.user = user; next(); 
});
```

Cuando el token es válido, guardas el usuario en `req.user` para que las siguientes funciones del _pipeline_ puedan acceder a esa información. Después llamas a `next()` y el flujo continúa.

> **¿Por qué guardar el secreto en variables de entorno?** Porque cualquiera con acceso al secreto puede generar tokens falsos válidos. Mantenerlo fuera del código y del repositorio protege tu aplicación.

## Cómo proteger una ruta usando el middleware authenticateToken

Una vez exportas la función con `module.exports = authenticateToken`, la importas en tu archivo principal `app.js` y la pasas como segundo argumento de cualquier ruta que quieras proteger.

```js 
const authenticateToken = require('./middlewares/auth');

app.get('/protectedRoute', authenticateToken, (req, res) => { 
	res.send('Esta es una ruta protegida'); 
});
```

El orden importa: Express ejecuta primero el _middleware_ y solo si llama a `next()` corre la función final que envía la respuesta.

## Cómo probar la ruta protegida en Postman

Para validar el comportamiento, abres Postman y creas una solicitud `GET` a `/protectedRoute`. En la pestaña **Headers** agregas `Authorization` con el valor `Bearer <token>`.

Prueba estos tres escenarios:

1. Sin header de Authorization: recibes `401 Access denied: No token provided`.
2. Con un token inventado: recibes `403 Invalid token`.
3. Con un token válido firmado con tu secreto: accedes al contenido de la ruta.

Esta prueba confirma que tu _middleware_ rechaza correctamente las solicitudes no autorizadas.

## Habilidades y conceptos clave que aparecen en la clase

Durante la implementación trabajas varias piezas que vale la pena tener claras.

- **Middleware** : función intermedia que se ejecuta entre la solicitud y la respuesta, ideal para validaciones.
- **Bearer token** : convención del header Authorization que antecede al token con la palabra `Bearer`.
- **process.env** : forma de leer variables de entorno en Node.js sin exponer secretos en el código.
- **Códigos HTTP 401 y 403** : diferencian entre falta de credenciales y credenciales inválidas.
- **req.user** : propiedad personalizada que transporta los datos del usuario autenticado al resto del flujo.