Express JS es el framework backend más usado dentro de Node JS y se ha convertido en el estándar para construir APIs y aplicaciones web. Aquí aprendes qué lo hace tan popular, cómo aprovechar sus principales características y cómo levantar tu primer servidor con un _Hello World_ funcional en minutos. Es ideal si vienes de JavaScript y quieres dar el salto al backend.

## ¿Por qué Express JS domina el backend con Node?

La respuesta corta: es minimalista, rápido y escalable. La respuesta larga tiene varias capas que vale la pena revisar.

Express JS sigue el principio _Don't Repeat Yourself_ y ofrece justo lo necesario para manejar solicitudes HTTP, integrar _middlewares_, definir rutas y construir lógica de negocio sin sentirte atado a un framework pesado. A diferencia de opciones más rígidas, te permite avanzar rápido sin sacrificar funcionalidad .

> **¿Qué es un middleware en Express JS?** Es una función que se ejecuta antes o después del ciclo de vida de tu API. Sirve para construir autenticación, _login_, validaciones y manejo de errores sin ensuciar tu lógica principal.

La escalabilidad tampoco es un problema. Hoy hay empresas que lo usan en productos empresariales que atienden a miles de usuarios, y brilla especialmente cuando necesitas:

- Crear _APIs REST_ limpias y mantenibles.
- Integrar tu backend con aplicaciones React u otros clientes.
- Construir _chatbots_ conectados a la API de WhatsApp e incluso a modelos de inteligencia artificial .

A esto súmale que corre sobre el motor V8 de Google, lo que potencia su rendimiento, y que tiene una comunidad enorme detrás, con paquetes y recursos para casi cualquier escenario.

## ¿Cómo configuro mi entorno para empezar con Express?

Antes de escribir código, necesitas preparar tu espacio de trabajo. La buena noticia es que toma menos de un minuto.

Abre tu terminal en la carpeta donde quieras trabajar y crea el directorio del proyecto. Luego entra en él e inicializa Git y npm para tener todo listo :

1. `mkdir curso-express-js` para crear la carpeta del proyecto.
2. `cd curso-express-js` para entrar en ella.
3. `git init` para inicializar el control de versiones.
4. `npm init -y` para generar el `package.json` con valores por defecto.
5. `npm install express --save` para instalar Express como dependencia.

Cuando termine la instalación, vas a ver que se agregaron alrededor de 14 paquetes. Eso significa que Express y sus dependencias ya están listos para usarse en tu proyecto.

> **¿Qué hace el flag `-y` en `npm init`?** Acepta automáticamente todas las preguntas de configuración con valores por defecto. Es la forma más rápida de generar tu `package.json` cuando estás prototipando.

## ¿Cómo creo mi primera API con Express JS?

Con el entorno listo, abre tu editor favorito (Visual Studio Code funciona perfecto) y crea un archivo llamado `app.js`. Ese va a ser el corazón de tu aplicación.

Importar Express e inicializar la app

Lo primero es traer Express al archivo y crear una instancia de la aplicación, además de definir el puerto donde va a escuchar .

```javascript 
const express = require('express'); 
const app = express(); 
const port = 3000;
```

Aquí `express()` es la función que inicializa tu aplicación, y `port` define en qué puerto va a estar disponible. El 3000 es una convención común en desarrollo local.

Definir tu primera ruta

Ahora viene lo interesante: registrar un _endpoint_. Vas a usar el método `get` de la app para responder en la ruta raíz (`/`).

```javascript 
app.get('/', (req, res) => { 
	res.send('Hello World'); 
});
```

El método `res.send` envía la respuesta al cliente. Puede ser un _string_, un HTML o un JSON, según lo que necesites devolver. En este caso, devuelves un _Hello World_ simple para validar que todo funciona.

Levantar el servidor

Para que tu aplicación responda peticiones, necesita estar escuchando en el puerto. Eso se hace con `app.listen` :

```javascript 
app.listen(port, () => { 
	console.log('Nuestra aplicación está funcionando'); 
});
```
Guarda el archivo, vuelve a la terminal y ejecuta `node app.js`. Vas a ver el mensaje en consola confirmando que el servidor está activo. Abre tu navegador, entra a `localhost:3000` y deberías ver tu _Hello World_ en pantalla.

> **¿Para qué sirve `app.listen` en Express?** Es el método que pone tu servidor a escuchar peticiones en un puerto específico. Sin él, tu aplicación se define pero nunca se ejecuta como servidor.

Desde aquí puedes empezar a sumar rutas, _middlewares_, conexión con bases de datos y toda la lógica que necesite tu producto. El verdadero poder de Express está en que te deja enfocarte en el modelo de negocio, no en pelear con el framework.

---

## 📂 Índice de Contenidos

- [[ExpressJs/Body Parser y Express API|Body Parser y Express API]]
- [[ExpressJs/Config|Config]]
- [[ExpressJs/Variables de Entorno|Variables de Entorno]]

### Crud
- [[ExpressJs/CRUD/Eliminar|Eliminar]]
- [[ExpressJs/CRUD/GET|GET]]
- [[ExpressJs/CRUD/Métodos HTTp y Crud|Métodos HTTp y Crud]]
- [[ExpressJs/CRUD/PUT|PUT]]
- [[ExpressJs/CRUD/Postman|Postman]]
- [[ExpressJs/CRUD/Procesamietno de Formularios y JSON con Body Parser|Procesamietno de Formularios y JSON con Body Parser]]
- [[ExpressJs/CRUD/Validaciones en POST y PUT|Validaciones en POST y PUT]]

### Desplegar
- [[ExpressJs/Desplegar/Desplegar DB|Desplegar DB]]
- [[ExpressJs/Desplegar/Desplegar la Api|Desplegar la Api]]

### Estructura
- [[ExpressJs/Estructura/Admin services|Admin services]]
- [[ExpressJs/Estructura/Controladores de Admin|Controladores de Admin]]
- [[ExpressJs/Estructura/Endpoint|Endpoint]]
- [[ExpressJs/Estructura/Modelacion de la DB|Modelacion de la DB]]
- [[ExpressJs/Estructura/Organización y estructuras|Organización y estructuras]]
- [[ExpressJs/Estructura/Refactorizacion|Refactorizacion]]
- [[ExpressJs/Estructura/Rutas y controladores|Rutas y controladores]]
- [[ExpressJs/Estructura/Servicios y Controladores|Servicios y Controladores]]

### Json Web Token (Jwt)
- [[ExpressJs/JSON Web Token (JWT)/Autenticación de Usuarios con JSON|Autenticación de Usuarios con JSON]]
- [[ExpressJs/JSON Web Token (JWT)/JWT|JWT]]
- [[ExpressJs/JSON Web Token (JWT)/Registrar Usuarios|Registrar Usuarios]]

### Middleware
- [[ExpressJs/Middleware/Crear Middleware|Crear Middleware]]
- [[ExpressJs/Middleware/Middleware de errores|Middleware de errores]]

### Db
- [[ExpressJs/db/Cargar Data en Prisma por seed|Cargar Data en Prisma por seed]]
- [[ExpressJs/db/PostgreSQL|PostgreSQL]]
- [[ExpressJs/db/Prisma|Prisma]]


---

[[Welcome|⬅️ Volver al Hub Principal]]
