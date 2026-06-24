La estructuración de aplicaciones backend es un elemento fundamental para garantizar la escalabilidad y mantenibilidad de nuestros proyectos. Cuando comenzamos a desarrollar, es común que todo nuestro código esté en un solo archivo, pero a medida que la aplicación crece, esta práctica se vuelve insostenible. Aprender a organizar correctamente nuestro código nos permitirá trabajar de manera más eficiente, especialmente en entornos colaborativos donde múltiples desarrolladores interactúan con el mismo proyecto.

## ¿Por qué es importante estructurar correctamente una aplicación backend?

Cuando una aplicación comienza a crecer, mantener todo el código en un solo archivo puede generar diversos problemas. Si analizamos detalladamente, veremos que tenemos muchas líneas de código que, aunque funcionan para aprender e integrar funcionalidades, no son óptimas para un producto o servicio real.

Para garantizar características importantes como:

- **Escalabilidad**: capacidad de crecer sin comprometer el rendimiento
- **Mantenibilidad**: facilidad para realizar cambios y correcciones
- **Colaboración**: permitir que varios desarrolladores trabajen simultáneamente

Es necesario separar nuestra aplicación en diferentes componentes, cada uno con una responsabilidad específica. Esta práctica no solo mejora la organización del código, sino que también reduce los conflictos cuando múltiples desarrolladores trabajan en el mismo proyecto.

## Creando una estructura de carpetas adecuada

El primer paso para estructurar correctamente nuestra aplicación es crear una carpeta llamada `src` (source), donde incorporaremos los elementos clave:

```js
proyecto/
├── src/
│   ├── middlewares/
│   ├── utils/
│   ├── controllers/
│   ├── services/
│   ├── routes/
│   ├── app.js
│   └── server.js
├── prisma/
├── node_modules/
├── .env
├── .gitignore
├── package.json
└── package-lock.json
```

Es importante destacar que carpetas como `prisma` no forman parte del código fuente de nuestra aplicación, sino que son recursos que utilizamos en modo desarrollo para migraciones y otras tareas. Por eso, no las incluimos dentro de `src`.

## ¿Cómo separar la lógica de nuestra aplicación en componentes?

Para estructurar correctamente nuestra aplicación, vamos a separar la lógica en diferentes archivos y carpetas según su responsabilidad:

### Separando el servidor de la aplicación

Primero, creamos dos archivos principales:

1. **server.js**: se encargará exclusivamente de levantar el servidor y configurar el puerto.

```javascript
const app = require('./app');
const port = process.env.PORT || 3000;

app.listen(port, () => {
  console.log(`Servidor ejecutándose en http://localhost:${port}`);
});
```

2. **app.js**: contendrá la configuración de Express y la conexión con las rutas.

```javascript
const express = require('express');
const routes = require('./routes');

const app = express();

app.use(express.json());
app.use('/api', routes);

app.get('/', (req, res) => {
  res.send('Hello World');
});

module.exports = app;
```

### Organizando las rutas

Dentro de la carpeta `routes`, creamos un archivo `index.js` que servirá como punto de entrada para todas nuestras rutas:

```javascript
const express = require('express');
const router = express.Router();
const authRoutes = require('./auth');

router.use('/auth', authRoutes);

module.exports = router;
```

Luego, creamos archivos específicos para cada grupo de rutas. Por ejemplo, para la autenticación:

```javascript
const express = require('express');
const router = express.Router();
const { register, login } = require('../controllers/authController');
const authenticateToken = require('../middlewares/auth');

router.post('/register', register);
router.post('/login', login);
router.get('/protected', authenticateToken, (req, res) => {
  res.json({ message: 'Esta es una ruta protegida', user: req.user });
});

module.exports = router;
```

## ¿Cuáles son las ventajas de utilizar controladores y servicios?

La separación de la lógica en controladores y servicios es una práctica recomendada que ofrece múltiples beneficios:

### Controladores

Los controladores se encargan de:

- Recibir las solicitudes HTTP
- Validar los datos de entrada
- Llamar a los servicios correspondientes
- Formatear y enviar las respuestas

### Servicios

Los servicios contienen:

- La lógica de negocio
- La comunicación con la base de datos
- Operaciones complejas
- Reglas específicas de la aplicación

**Esta separación permite:**

- **Mayor claridad**: cada componente tiene una responsabilidad específica
- **Facilidad de pruebas**: podemos probar cada componente de manera aislada
- **Reutilización de código**: los servicios pueden ser utilizados por diferentes controladores
- **Mantenimiento simplificado**: los cambios en la lógica de negocio no afectan a la interfaz de la API

Al estructurar nuestra aplicación de esta manera, estamos siguiendo el principio de responsabilidad única, donde cada componente tiene una única razón para cambiar.

## Implementando controladores

En la carpeta `controllers`, creamos archivos específicos para cada grupo de funcionalidades. Por ejemplo, para la autenticación:

```javascript
const authService = require('../services/authService');

const register = async (req, res) => {
  try {
    const user = await authService.createUser(req.body);
    res.status(201).json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
};

const login = async (req, res) => {
  try {
    const { token, user } = await authService.loginUser(req.body);
    res.json({ token, user });
  } catch (error) {
    res.status(401).json({ error: error.message });
  }
};

module.exports = {
  register,
  login
};
```

La estructuración adecuada de una aplicación backend es un paso fundamental para garantizar su éxito a largo plazo. Al separar nuestro código en componentes con responsabilidades específicas, no solo mejoramos la organización, sino que también facilitamos el mantenimiento y la colaboración entre desarrolladores. **¿Has tenido experiencias con aplicaciones mal estructuradas? ¿Qué otros patrones de organización has utilizado en tus proyectos?** Comparte tus experiencias en los comentarios.