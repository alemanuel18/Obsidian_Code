Cuando prototipas una API y aún no tienes base de datos ni lógica conectada, necesitas una forma de entregarle al equipo mobile y front-end algo funcional para que avancen sin esperarte. Aquí entra el concepto de **mock de API con OpenAPI**, una técnica que te permite simular respuestas reales a partir de la estructura definida en tu documento, sin escribir una sola línea de código en Express.

Esta práctica es clave para equipos de desarrollo que trabajan en paralelo y necesitan integraciones tempranas mientras el back-end termina de definir costes en la nube, base de datos y lógica interna.

## Por qué usar un mock cuando todavía no tienes la API lista

El objetivo es no detener al equipo. Mientras tú terminas de prototipar y validar la implementación, el front-end y mobile ya pueden empezar a integrar contra una API simulada que devuelve datos ficticios alineados a la estructura final.

El documento OpenAPI cumple un rol central: define cada endpoint, sus validaciones y particularidades. Ese mismo archivo se convierte en la fuente única de verdad que el equipo puede consumir desde el día uno.

> **¿Qué es un mock de API?** Es un servidor simulado que responde con datos ficticios basados en la estructura de tu documento OpenAPI, sin tener lógica ni base de datos detrás.

El día que la API real esté desplegada, lo único que cambia para el equipo es el _endpoint_ principal. La estructura de las respuestas se mantiene idéntica.

## Cómo instalar Prism CLI para levantar un mock server

La herramienta que usamos para esto es Prism, de Stoplight. Es un paquete que lee tu archivo OpenAPI y levanta un servidor mock automáticamente, sin que tengas que codear nada en Express.

Para instalarlo, abre tu terminal y ejecuta el comando como paquete global:

```bash 
npm install -g @stoplight/prism-cli
```

Una vez instalado, ya puedes generar un mock a partir de cualquier archivo OpenAPI que tengas en la raíz de tu proyecto.

## Qué comando ejecutar para generar el mock

Desde la raíz del proyecto donde vive tu archivo OpenAPI, corre el comando que activa el servidor de simulación apuntando al archivo de definición.

```bash 
prism mock openapi.yaml
```

Al darle enter, Prism habilita los endpoints definidos en el documento. Vas a ver en consola las rutas disponibles: el `hello`, el `user` con un ID generado automáticamente, los métodos POST y los demás recursos que hayas declarado.

> **¿Para qué sirve Prism CLI?** Sirve para levantar un servidor mock a partir de un archivo OpenAPI, devolviendo datos ficticios con la misma estructura que tendrá la API real cuando esté lista.

## Cómo validar que el mock funciona y leer el log de peticiones

Una vez levantado el servidor, puedes abrir el navegador y consultar cualquiera de los endpoints. Por ejemplo, al entrar a `/users` recibes una respuesta con un usuario ficticio: un _id_ en cero, un _string_ de ejemplo y los campos definidos en el esquema.

En la terminal vas a ver un log completo con el histórico de peticiones. Ese log te muestra:

- Qué endpoints están siendo consultados.
- Qué método HTTP se está utilizando.
- Si la respuesta cumple con el esquema definido.
- Errores de validación si los hay.

Esto es útil para que el equipo que consume la API detecte rápido si está enviando datos en el formato correcto, sin necesidad de tener al back-end disponible.

## Qué entregar al equipo de front-end y mobile

No necesitas compartirles un repositorio con código de servidor ni desplegar nada. Lo único que necesitan es el archivo OpenAPI.

### Con ese archivo, ellos mismos pueden:

- Instalar Prism con un solo comando.
- Levantar su propio mock local.
- Empezar a integrar la API en sus aplicaciones mobile o web.
- Ver el log completo de sus peticiones.

> **¿Qué le entrego al equipo si todavía no tengo la API construida?** Solo el archivo OpenAPI. Con ese documento y Prism, cualquier desarrollador puede levantar un mock funcional en segundos.

La ventaja real es que **el equipo trabaja de forma uniforme**: el back-end avanza con la implementación seria mientras front-end y mobile ya están integrando contra una estructura confiable. Cuando llega el momento de conectar con la API real, el cambio es mínimo, solo se actualiza la URL base.

Esta forma de trabajar también deja claro algo importante sobre el flujo profesional: aunque puedas pedirle a una inteligencia artificial que te genere mocks locales para validar avances, lo recomendable es que tu archivo OpenAPI tenga primero todos los puntos de entrada bien definidos. Esa disciplina te ahorra retrabajo y mantiene a todo el equipo alineado.