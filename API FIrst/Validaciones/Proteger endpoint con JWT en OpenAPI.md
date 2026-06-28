Diseñar una API sin pensar en seguridad es como abrir la puerta de tu casa y dejar las llaves puestas. Por eso, dentro del archivo de especificación **OpenAPI** puedes declarar la autenticación con **JSON Web Token (JWT)** y que la documentación refleje qué endpoints están protegidos y cuáles no. Esta guía te muestra cómo hacerlo paso a paso, ideal si estás construyendo APIs y quieres documentar su seguridad desde el inicio.

## ¿Cómo se define la seguridad dentro del archivo OpenAPI?

La seguridad en OpenAPI vive en la sección de _components_, donde declaras un _security scheme_ reutilizable que luego puedes invocar en cualquier endpoint.

Dentro de _components_ agregas el bloque _securitySchemes_ y defines el método de autenticación que vas a usar. Para JWT necesitas especificar:

- El **type**, que indica el tipo de esquema de autenticación.
- El **scheme**, que define el manejo del esquema.
- El **bearerFormat**, que describe el formato del token, en este caso JWT.
- Una **description** breve para que cualquiera entienda qué hace ese componente.

Con esto ya tienes un componente reutilizable. Cada vez que quieras pedir autenticación en un endpoint, solo lo referencias y listo, no tienes que reescribir la configuración.

> **¿Qué es un security scheme en OpenAPI?** Es un componente reutilizable dentro de _components_ que define cómo se autentica una API. Puedes declarar JWT, API keys, OAuth2 y otros métodos, y luego aplicarlos a los endpoints que quieras proteger.

## ¿Por qué declarar la seguridad a nivel global?

Después de definir el _securitySchemes_, agregas también el path _security_ a nivel raíz del documento. Eso le indica al estándar OpenAPI que tu API, por defecto, espera un JSON Web Token. Después puedes sobrescribir esta regla endpoint por endpoint si alguno necesita ser público.

## ¿Cómo crear un endpoint de autenticación con JWT?

Una vez que tienes el esquema definido, necesitas un punto de entrada que entregue el token al usuario que se autentica correctamente.

Aquí entra una ventaja interesante: puedes apoyarte en herramientas de inteligencia artificial como **Cursor** o **ChatGPT** seleccionando el _schema_ de seguridad y pidiéndole algo como _crea un endpoint para autenticar los usuarios con la implementación de OpenAPI utilizando JSON Web Token_. La herramienta interpreta el contexto de tu documento y propone la estructura.

El resultado típico incluye:

- Un endpoint **POST /auth/login** categorizado dentro de _usuarios_.
- Un **request body** con las propiedades de email y contraseña, junto con sus validaciones.
- Un **content** con _application/json_ y un _schema_ asociado.
- La respuesta con las credenciales y el token generado.

Un detalle importante: revisa siempre lo que te entrega la IA. No siempre es la solución más correcta, pero acelera la documentación y evita que se te olviden elementos. Si vas a tener varios endpoints relacionados con usuario y contraseña, lleva ese _schema_ a un componente reutilizable para no duplicar código.

## ¿Cómo proteger endpoints específicos como productos?

No todas las rutas deben ser públicas. Listar productos en una tienda puede ser abierto, pero **crear, modificar o eliminar** un producto es crítico y necesita autenticación.

La forma de aplicarlo es directa: en cada endpoint sensible añades la propiedad _security_ haciendo referencia al esquema JWT que ya definiste. Puedes pedírselo a tu asistente de IA con un prompt como _actualiza el documento de OpenAPI para que los endpoints de productos estén protegidos y solo usuarios autenticados puedan hacer solicitudes PUT, POST y DELETE_.

La lógica que se aplica suele ser esta:

1. **GET /products** queda público para que cualquiera pueda listar.
2. **POST /products** exige JWT en los headers para crear.
3. **PUT /products/{id}** exige JWT para modificar.
4. **DELETE /products/{id}** exige JWT para eliminar.

Cuando levantas el servidor con _npm run dev_ y abres la documentación, vas a ver un **candado** al lado de los endpoints protegidos. Ese candado significa que el endpoint requiere un token válido en los parámetros de autorización para responder.

> **¿Qué significa el candado en Swagger o la documentación OpenAPI?** Indica que ese endpoint requiere autenticación. Para probarlo, necesitas pegar un JSON Web Token válido en el campo de autorización antes de enviar la solicitud.

## ¿Cómo probar los endpoints protegidos?

Una vez generado el token desde _POST /auth/login_, lo copias y lo pegas en el valor de autorización de la documentación interactiva. A partir de ahí, todas las pruebas que hagas a endpoints protegidos viajarán con ese JWT en los headers, validando que tienes permiso para ejecutar la operación.

Un buen hábito mientras desarrollas: aunque el servidor escuche cambios en caliente, mátalo y vuelve a inicializarlo cuando modificas el archivo OpenAPI. Así te aseguras de que la documentación refleje la versión más reciente.

Documentar seguridad en OpenAPI no es un extra estético, es parte del contrato de tu API. Cuando otro desarrollador, un cliente o tu yo del futuro abra el documento, sabrá exactamente qué endpoints son públicos, cuáles exigen JWT y cómo obtener ese token.