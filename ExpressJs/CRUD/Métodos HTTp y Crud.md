Construir una **API RESTful** es lo que le da sentido a trabajar con Express.js. Aquí aprendes qué significa REST, cómo funcionan los métodos HTTP (GET, POST, PUT, PATCH, DELETE) y por qué son la base de cualquier aplicación web moderna que separe backend y frontend.

## Qué significa REST y por qué importa en Express.js

REST viene de _Representational State Transfer_, un conjunto de principios que facilita la comunicación con servicios web. La idea es simple: aprovechar los protocolos HTTP y usar verbos específicos para definir cómo interactúas con la información.

Cuando desarrollas una aplicación web, normalmente separas la lógica en dos piezas. Por un lado tienes el **backend**, donde vive tu API RESTful. Por el otro, el **frontend**, que consume e interactúa con esa API. Esa separación es la que hace todo escalable y mantenible .

> **¿Qué es una API RESTful?** Es una interfaz que sigue los principios REST y usa métodos HTTP para que un cliente (como tu frontend) se comunique con un servidor de forma estándar.

## Cuáles son los métodos HTTP más usados en una API

Los verbos HTTP son las acciones que defines sobre tus recursos. Algunos ya los has tocado, otros son nuevos, pero juntos forman el corazón de cualquier API .

## Cómo funcionan GET y POST en una API

El método **GET** se usa para solicitar un recurso específico al servidor. Entras a una URL y el servidor te responde con información: puede ser un HTML, un JSON o cualquier formato que hayas especificado en el punto de entrada .

El método **POST** se usa para enviar datos al servidor que serán procesados o almacenados. Aquí entran casos clásicos como:

- Enviar usuario y contraseña para autenticarte en un panel administrativo.
- Guardar información de un formulario en una base de datos.
- Procesar la selección de inputs de un sitio web.

Estos dos son los más comunes que vas a encontrar al trabajar con APIs.

## Para qué sirven PUT, PATCH y DELETE

Aquí es donde la API se vuelve completa. Estos tres métodos te dan control total sobre la información que ya existe en el servidor.

- **PUT**: actualiza o reemplaza completamente un recurso existente. Imagina que creaste un usuario y notas que el nombre tiene un error. Con PUT actualizas toda la información del recurso de una sola vez.
- **PATCH**: realiza una actualización parcial. Solo quieres cambiar un ID o un valor puntual sin tocar el resto del recurso. Este método tiene su asterisco porque trabaja distinto a PUT.
- **DELETE**: el nombre lo dice todo. Elimina el recurso existente que estás indicando en la solicitud.

> **¿Cuál es la diferencia entre PUT y PATCH?** PUT reemplaza el recurso completo, mientras que PATCH solo modifica los campos específicos que envías. Si vas a cambiar todo, usa PUT. Si solo cambias una parte, usa PATCH.

##  es CRUD y cómo se relaciona con los verbos HTTP

Cuando juntas estos métodos, llegas al concepto de **CRUD**: _Create, Read, Update y Delete_. Son las cuatro operaciones básicas que cualquier aplicación necesita para gestionar información .

La relación con los verbos HTTP es directa:

- **Create** se mapea con POST.
- **Read** se mapea con GET.
- **Update** se mapea con PUT o PATCH.
- **Delete** se mapea con DELETE.

A partir de aquí vas a construir un CRUD completo usando una API. El proyecto principal será un **sistema de booking**, donde aplicarás cada uno de estos verbos en escenarios reales y los probarás con **Postman**, la herramienta favorita para validar endpoints .

> **¿Qué es Postman y para qué se usa?** Es una herramienta que te permite enviar solicitudes HTTP a tu API sin necesidad de un frontend. Sirve para probar que cada endpoint responda correctamente antes de conectarlo con el cliente.

## Qué viene después de entender los métodos HTTP

Con estos conceptos claros, el siguiente paso es entrar en las particularidades de cada método: cómo configurarlos en Express.js, qué puedes hacer con cada uno y cómo probarlos directamente. La arquitectura de una API RESTful, los recursos HTTP y la estructura de las solicitudes son la base que vas a usar en cada clase .

En la siguiente clase empiezas a construir un punto de entrada para solicitudes GET. ¿Ya tienes claro qué método usarías para cada parte de tu sistema de booking? Cuéntame en los comentarios cómo estructurarías tu primer endpoint.