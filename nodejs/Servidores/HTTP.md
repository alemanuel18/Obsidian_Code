Crear un **servidor HTTP en Node.js** es uno de los primeros pasos para entender cómo funcionan las aplicaciones web del lado del backend. Con el módulo nativo `http` puedes levantar un server, responder peticiones y escuchar en un puerto sin instalar dependencias externas, ideal si estás aprendiendo a construir APIs desde cero.

## ¿Qué hace el módulo http de Node.js?

El módulo `http` viene incluido en Node.js y te permite crear tanto servidores como clientes que se comuniquen mediante el protocolo HTTP. No necesitas instalar nada extra, solo importarlo con `require`.

> **¿Qué es el módulo http en Node.js?** Es un módulo nativo que permite crear servidores y clientes HTTP. Lo importas con `const http = require('http')` y te da acceso a métodos como `createServer` para responder peticiones .

## ¿Cómo se estructura un server básico?

La receta mínima para tener un servidor funcional usa `http.createServer`, que recibe una función con dos parámetros: `request` y `response`. Dentro defines qué responder cuando alguien llegue a tu endpoint.

```javascript 
const http = require('http');

const server = http.createServer((req, res) => { res.writeHead(200, { 'Content-Type': 'text/plain' }); res.end('Hello World'); });

server.listen(3000, 'localhost', () => { console.log('Server running'); });
```

Aquí pasan tres cosas clave:

- `res.writeHead(200, ...)` envía el **status code 200** y define el `Content-Type` como `text/plain` .
- `res.end('Hello World')` cierra la respuesta enviando el texto al cliente .
- `server.listen(3000, 'localhost', ...)` deja al servidor escuchando en el puerto 3000 .

## ¿Por qué localhost a veces no funciona y aparece not found?

Cuando ejecutas el server y abres `localhost:3000` en el navegador, puede aparecer un error `not found`. Esto ocurre porque, dependiendo de cómo configures el `listen`, Node puede estar escuchando en `127.0.0.1` y no reconocer el alias `localhost` directamente .

La solución es pasar explícitamente `'localhost'` como segundo argumento de `server.listen`, o bien acceder directamente con la IP `127.0.0.1:3000`. Ambas rutas apuntan al mismo lugar, pero el navegador necesita coincidencia exacta con lo que el server declara.

> **¿Cuál es la diferencia entre localhost y 127.0.0.1?** Ambas referencian tu máquina local, pero `localhost` es un nombre de host y `127.0.0.1` es la dirección IP. Node escucha en una u otra según cómo configures `listen`.

## ¿Cómo recargar el servidor automáticamente con el flag watch?

Durante años, los desarrolladores de Node usaron **Nodemon** para reiniciar el server cada vez que guardaban un cambio. Desde la **versión 18 de Node.js**, esto ya no es necesario: existe el flag `--watch`, que entró como beta y escucha modificaciones en tu script para reejecutarlo automáticamente .

Para usarlo solo necesitas correr:

bash node --watch server.js

Puedes verificar tu versión de Node con `node -v`. Si tienes la 18 o superior (en la clase se usa la 23), tienes acceso al flag sin instalar nada .

## ¿Qué ventaja tiene watch frente a Nodemon?

La diferencia práctica es que ya no dependes de un paquete externo:

1. No necesitas instalar Nodemon vía npm.
2. No agregas dependencias a tu `package.json`.
3. El comportamiento es nativo y mantenido por el equipo de Node.

Cada vez que guardas un cambio, por ejemplo modificar el texto `Hello World`, el server se reinicia solo y refrescas el navegador para ver el resultado . Te olvidas del clásico Ctrl+C para matar el proceso y volver a levantarlo.

## ¿Cuándo conviene usar http puro y cuándo Express.js?

El módulo `http` es perfecto para entender los fundamentos: cómo se forma una respuesta, qué es un status code, cómo se define un `Content-Type`. Pero cuando empiezas a construir APIs con varias rutas, middlewares y manejo de errores, escribir todo a mano se vuelve tedioso.

Ahí entra **Express.js**, un framework que se monta sobre el módulo `http` y te da una sintaxis mucho más amigable para definir endpoints, manejar parámetros y organizar tu código. No reemplaza a HTTP, lo encapsula.

> **¿Express.js sustituye al módulo http?** No. Express usa internamente el módulo `http` de Node, pero te ofrece una API más sencilla para crear rutas, middlewares y respuestas estructuradas.