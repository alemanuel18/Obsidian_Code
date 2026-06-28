Desarrollar una API efectiva implica mucho más que simplemente escribir código. Se requieren procesos claros para su construcción y documentación. Hoy aprenderás cómo estructurar y crear una API con Express en Node.js, definir sus puntos de entrada y generar automáticamente su documentación visual usando Swagger y OpenAPI.

## ¿Cómo crear una API básica con Express y Node.js?

Express es un marco de trabajo sencillo y potente en Node.js que facilita la construcción de APIs de manera rápida y eficiente. Para comenzar, sigue estos pasos esenciales:

- Define la constante `express` e instancia un objeto para ejecutar tu servidor:

```javascript
const express = require('express');
const app = express();
```

- Configura un puerto para mostrar tu servidor (comúnmente, el 3000):

```javascript
const port = 3000;

app.listen(port, () => {
  console.log(`Servidor funcionando en puerto ${port}`);
});
```

## ¿Cómo definir y probar un endpoint básico?

Una vez listo el servidor, el siguiente paso es añadir puntos de entrada o endpoints que manejen solicitudes específicas del usuario:

- Crear un endpoint sencillo que responda con JSON al visitar la ruta `/hello`:

```javascript
app.get('/hello', (req, res) => {
  res.json({ message: "hello world" });
});
```

- Puedes arrancar tu servidor usando un _script_ personalizado incluidos en los `scripts` de `package.json`, para reflejar automáticamente cambios en tu código:

```json
"scripts": {
    "dev": "node --watch index.js"
}
```

Esto aprovecha una funcionalidad nativa y reciente de Node.js, por lo que no necesitas instalar herramientas adicionales como Nodemon.

## ¿Cómo documentar y visualizar tu API con Swagger y OpenAPI?

Utilizar Swagger para documentar tu API permite visualizar puntos de entrada, parámetros necesarios y respuestas esperadas de una forma clara en un navegador web:

- Instala y configura Swagger UI y YAML previamente:

```javascript
const swaggerUi = require('swagger-ui-express');
const YAML = require('yamljs');
const swaggerDocument = YAML.load('./openapi.yaml');

app.use('/docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```

- Accede a la documentación visual desde tu navegador ingresando a `localhost:3000/docs`. Esta herramienta te permite visualizar claramente cómo interactuar con tu API:
    
    - Probar directamente endpoints desde la documentación visual.
    - Ver respuestas y códigos de estado HTTP claramente organizados.
    - Facilitar la interacción y desarrollo colaborativo al proporcionar documentación organizada y fácilmente accesible.

## ¿Qué herramientas adicionales usamos para ver JSON fácilmente en el navegador?

Durante el desarrollo y prueba de APIs puedes usar plugins útiles para tu navegador:

- JSON Viewer Pro (un plugin para Chrome), que permite visualizar y manipular fácilmente respuestas en formato JSON.
- Este complemento ayuda a probar e interactuar con tu API de un modo claro y organizado, ofreciendo opciones como exportación y análisis fácil de respuestas.