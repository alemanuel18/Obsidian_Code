Si estás construyendo una API REST y aún no quieres conectarte a una base de datos, puedes usar el método **GET en Node.js** para leer datos desde un archivo JSON local. Esta práctica te prepara para escalar tu proyecto sin perder claridad en la lógica.

## Cómo configurar Node.js para leer archivos locales

Antes de programar el endpoint, necesitas habilitar tu proyecto para trabajar con el sistema de archivos. Node.js trae módulos nativos que hacen este trabajo sin instalar dependencias extra.

El módulo _fs_ (file system) se encarga de leer y escribir archivos, mientras que _path_ maneja las rutas de forma segura entre distintos sistemas operativos. Los importas así:

```javascript 
const fs = require('fs'); const path = require('path');
```

> **¿Qué hace el módulo fs en Node.js?** Es el módulo nativo que permite interactuar con el sistema de archivos: leer, escribir, crear y eliminar archivos directamente desde tu servidor.

## Por qué crear un archivo users.json como base local

En la raíz del proyecto se crea un archivo `users.json` que actúa como una mini base de datos. Contiene una estructura simple con campos como id, nombre y email para dos usuarios de prueba.

La ruta hacia ese archivo se construye con `path.join` y `__dirname`, que apunta al directorio actual:

```javascript 
const usersFilePath = path.join(__dirname, 'users.json');
```

Esta lógica es prácticamente la misma que vas a usar cuando migres a una base de datos real. Solo cambia la fuente: en lugar de leer un archivo local, harás una conexión externa.

## Cómo construir un endpoint GET en Express paso a paso

Con la configuración lista, defines la ruta `/users` usando `app.get`. Recibes los parámetros _req_ y _res_, y dentro del callback ejecutas la lectura del archivo.

El método `fs.readFile` recibe tres argumentos clave:

- La ruta del archivo, en este caso `usersFilePath`.
- La codificación, que será _UTF-8_ para leer texto plano.
- Una función anónima con dos parámetros: _error_ y _data_.

```javascript 
app.get('/users', (req, res) => { 
	fs.readFile(usersFilePath, 'utf-8', (error, data) => { 
		 if (error) { 
			 return res.status(500).json({ error: 'Error con la conexión de datos' }); 
		} 
		const users = JSON.parse(data); res.json(users); 
	}); 
});
```

## Cómo manejar errores con códigos de estado HTTP

Nunca asumas que la lectura va a salir bien. Si el archivo no existe o hay un problema de permisos, tu API debe responder de forma clara.

Por eso se valida primero el parámetro _error_. Si existe, retornas un `res.status(500)` con un mensaje en JSON. El código **500 indica un error del servidor**, perfecto para fallos como una conexión fallida o un archivo no encontrado.

> **¿Por qué usar JSON.parse al leer un archivo?** Porque `fs.readFile` devuelve los datos como texto plano. Para manipularlos como objeto JavaScript necesitas convertirlos con `JSON.parse(data)`.

Escapar y validar la información protege tu aplicación y mantiene al usuario informado sobre lo que está pasando, en lugar de mostrar errores crípticos.

## Cómo probar tu API GET en el navegador y en Postman

Una vez levantado el servidor con `npm run dev`, puedes acceder directamente desde el navegador a la ruta `/users`. Como GET es el método por defecto del navegador, verás el JSON renderizado en pantalla.

Para una experiencia más legible existen plugins de Chrome que formatean automáticamente las respuestas JSON. Te ayudan a iterar y explorar la estructura de los datos sin esfuerzo extra.

## Por qué documentar tus endpoints en Postman

Postman permite organizar tus requests en colecciones. Crear una colección llamada **API users** te da un espacio para guardar cada endpoint con su método, parámetros y respuestas esperadas.

Las ventajas de trabajar con colecciones son varias:

- Separas las pruebas por recurso o funcionalidad.
- Documentas cada request con descripciones y ejemplos.
- Compartes la colección con tu equipo para acelerar el desarrollo.
- Reutilizas configuraciones para distintos entornos.