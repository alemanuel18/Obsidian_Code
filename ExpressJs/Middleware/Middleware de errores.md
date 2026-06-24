Cuando construyes una API con Express, los errores son inevitables: una conexión fallida a la base de datos, un servidor lento o una petición mal formada pueden romper el flujo. Crear un _middleware_ de manejo de errores te permite capturar esas fallas, registrarlas y devolver respuestas claras al cliente sin exponer detalles sensibles. Esta guía es para desarrolladores que ya trabajan con Node y quieren un patrón sólido para producción.

## Qué hace un middleware de errorHandle en Express

Un _middleware_ de errores centraliza la captura de excepciones que ocurren en cualquier parte del ciclo de vida de la petición. En lugar de repetir bloques `try/catch` en cada ruta, delegas la respuesta a una sola función que decide qué mostrar según el entorno.

> **¿Qué es un middleware de manejo de errores?** Es una función con la firma `(err, req, res, next)` que Express reconoce automáticamente para procesar errores y devolver una respuesta estandarizada al cliente.

La firma con cuatro parámetros es la señal que Express usa para diferenciar este _middleware_ de los normales. Si omites el parámetro `err`, Express lo trata como un _middleware_ común y nunca recibirá los errores.

## Cómo construir el archivo errorHandle.js paso a paso

Dentro de la carpeta `middlewares`, crea el archivo `errorHandle.js`. La función necesita acceder al error, a la petición, a la respuesta y a `next` para mantener el flujo intacto.

```js 
function errorHandle(err, req, res, next) {
	const statusCode = err.statusCode || 500; 
	const message = err.message || 'Ocurrió un error inesperado';
	
	console.error(
		`Hubo un error ${new Date().toISOString()} ${statusCode} ${message}`
	);
	
	if (err.stack) { 
		console.error(err.stack); 
	}
	
	const { NODE_ENV } = process.env;
	
	res.status(statusCode).json({ 
		status: 'error', 
		statusCode, 
		message, 
		...(NODE_ENV === 'development' && { stack: err.stack }) 
	}); 
}

module.exports = errorHandle;
```

## Por qué usar 500 como status code por defecto

Cuando el error no trae un `statusCode` propio, asumir 500 tiene sentido porque la mayoría de fallas no controladas vienen del servidor: tiempos de espera, conexiones caídas o lógica que no contempló un caso. El usuario no provocó directamente ese error, así que la categoría correcta es _Internal Server Error_.

## Cómo registrar el stack trace para depurar

La propiedad `err.stack` contiene la traza completa: archivo, línea y secuencia de llamadas que llevaron al error. Imprimirla con `console.error` te da contexto suficiente para reproducir el problema en local sin tocar el código de producción.

## Cómo usar NODE_ENV para diferenciar desarrollo y producción

La variable de entorno `NODE_ENV` controla cuánta información expones en la respuesta. En desarrollo quieres ver el _stack_ completo; en producción, solo un mensaje genérico.

- **development**: muestra mensaje, status code y stack trace en la respuesta JSON.
- **production**: oculta el stack y devuelve solo el mensaje base.
- **staging**: entorno intermedio para pruebas previas al despliegue.

> **¿Por qué no mostrar el stack en producción?** Exponer rutas internas, nombres de archivos o lógica del servidor facilita ataques. El usuario final solo necesita saber que algo falló, no cómo está construida tu aplicación.

Declara `NODE_ENV=development` en tu archivo `.env` local y deja el `.env.example` vacío para que quien clone el repositorio decida su valor. Recuerda que cambiar variables de entorno requiere reiniciar el servidor con `npm run dev`.

## Cómo integrar el middleware en app.js

Importa el _middleware_ junto a los demás y regístralo con `app.use` después de las rutas, para que Express lo invoque cuando alguna ruta llame a `next(err)`.

```js 
const errorHandle = require('./middlewares/errorHandle');
app.use(errorHandle);
```

Para probarlo sin esperar a que ocurra un fallo real, agrega un _endpoint_ temporal que dispare un error a propósito. Este punto de entrada nunca debe llegar a producción.

```js 
app.get('/error', (req, res, next) => { 
	next(new Error('Error intencional')); 
});
```

Al visitar `/error` desde el navegador o Postman en modo development, verás la respuesta JSON con `statusCode`, `message` y `stack`. Cambia `NODE_ENV` a `production`, reinicia el servidor y la misma ruta devolverá únicamente _Internal Server Error_, mientras que la consola del servidor seguirá mostrando _Error intencional_ con su traza completa.

## Buenas prácticas al manejar errores en una API

Mantén separado lo que ve el usuario de lo que ve el equipo técnico. Esa frontera es la que protege tu sistema y mejora la experiencia.

- Define mensajes por defecto claros para cuando el error no traiga descripción.
- Usa `console.error` con timestamp ISO para ordenar logs cronológicamente.
- Valida siempre `err.stack` antes de imprimirlo, no todos los errores lo incluyen.
- Activa `development` solo en local; en servidores productivos usa `production`.
- Centraliza la respuesta JSON para que tu API sea consistente en cada fallo.