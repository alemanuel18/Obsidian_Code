Crear tu propio paquete npm en Node.js es más sencillo de lo que parece, y aquí vas a construir uno desde cero llamado _platzi-date_. La meta: manejar fechas en dos formatos útiles, _timestamp_ y _long time_, y dejarlo listo para probarlo localmente antes de publicarlo. Si estás aprendiendo Node.js y quieres entender el flujo real de empaquetar código reutilizable, este recorrido te va a servir.

## ¿Qué necesitas antes de crear un paquete npm?

Antes de escribir una sola línea de código, conviene preparar la estructura del proyecto en una carpeta independiente del resto de tus ejercicios.

Desde la terminal, crea la carpeta con `mkdir platzi-date` y entra en ella. Inicializa el control de versiones con `git init` y luego ejecuta `npm init -y` para generar un _package.json_ con la configuración por defecto, que después modificarás según las necesidades del paquete .

> **¿Qué hace npm init -y?** Crea automáticamente el archivo _package.json_ con valores por defecto, sin preguntarte campo por campo. Es ideal para arrancar rápido y ajustar después.

Luego, dentro del editor de código, crea una carpeta `src` y dentro un archivo `index.js`. Ahí va a vivir el código fuente del paquete.

## ¿Cómo construir las funciones para timestamp y fecha larga?

El paquete expone dos funciones específicas, cada una con una responsabilidad clara.

## La función getTimestamp

Esta función devuelve el timestamp actual usando `Date.now()`. Es directa: solo retorna el número de milisegundos desde el 1 de enero de 1970. Más adelante puedes formatearla según el caso de uso .

js function getTimestamp() { return Date.now(); }

## La función getLongTime

Esta es más interesante porque acepta un parámetro `locale` con valor por defecto en español, lo que la hace flexible para distintos idiomas y regiones.

Dentro defines una constante `options` con la configuración del formato:

- `weekday: 'long'` para el día de la semana completo.
- `year: 'numeric'` para el año en número.
- `month: 'long'` para el mes con nombre completo.
- `day: 'numeric'` para el día numérico.
- `hour`, `minute` y `second` en formato `numeric`.
- `timeZoneName: 'short'` para mostrar la zona horaria abreviada.

Luego retornas `new Date().toLocaleDateString(locale, options)`, que es el método nativo de JavaScript que aplica esa configuración al objeto `Date` .

Finalmente, expones ambas funciones con `module.exports = { getTimestamp, getLongTime }`.

## ¿Cómo configurar el package.json y el README?

Un paquete sin documentación clara y metadatos correctos no llega lejos. npm usa esta información para mostrarla en _npmjs.org_.

Crea un archivo `README.md` con el nombre del paquete, una descripción corta como _una utilidad para manejar fechas en formato timestamp y long time_, y un bloque de instalación en bash:

bash npm install platzi-date

En el `package.json` ajusta:

- El campo `main` para que apunte a `src/index.js`.
- Las `keywords` con valores como `date` y `nodejs` para mejorar descubrimiento.
- Tu nombre en `author` para que puedan contactarte.
- La `license` como `MIT`.
- Una `description` unificada con la del README.

> **¿Para qué sirven las keywords en package.json?** Ayudan a que tu paquete aparezca en búsquedas dentro del registro de npm. Son etiquetas que describen el propósito del paquete.

## ¿Cómo probar el paquete localmente sin publicarlo?

Aquí entra una de las herramientas más útiles del flujo de desarrollo en Node.js: _npm link_. Te permite usar tu paquete en otro proyecto como si ya estuviera publicado, pero apuntando a tu código local.

Desde la carpeta del paquete, ejecuta `npm link`. Esto crea un enlace simbólico en el sistema que registra tu paquete a nivel global .

Luego ve al proyecto donde quieres consumirlo y ejecuta `npm link platzi-date`. Eso conecta el paquete local con la carpeta `node_modules` de ese proyecto, sin necesidad de hacer `npm install`.

> **¿Qué es un enlace simbólico en npm link?** Es una referencia que apunta desde _node_modules_ a la carpeta real de tu paquete. Cualquier cambio que hagas en el código fuente se refleja al instante en el proyecto que lo consume.

## Probando el paquete con un archivo de pruebas

Crea un archivo `date.js` en tu proyecto principal y trae el paquete con:

js const dateFormat = require('platzi-date');

console.log('timestamp:', dateFormat.getTimestamp()); console.log('fecha en español:', dateFormat.getLongTime()); console.log('fecha en inglés:', dateFormat.getLongTime('en-US'));

Al correr `node date.js` deberías ver el timestamp en milisegundos, la fecha en español como _miércoles 26 de febrero_, y la versión en inglés con el formato regional de Estados Unidos .

Este flujo de validación local es clave: te asegura que el paquete funciona antes de publicarlo y evita subir versiones rotas al registro público.