Los módulos en Node.js son bloques de código encapsulados con una funcionalidad específica que puedes reutilizar en tus aplicaciones. Pensarlos como **piezas de Lego** ayuda: cada pieza resuelve algo puntual y la combinas para construir programas robustos, fáciles de mantener y libres de conflictos.

## ¿Qué son los módulos en Node.js y por qué importan?

Un módulo es una unidad de código que expone funciones, objetos o valores para que otros archivos los usen. Esa separación facilita el mantenimiento, evita repetir lógica y permite escalar proyectos sin que todo viva en un solo archivo.

> **¿Qué es un módulo en Node.js?** Es un archivo de código encapsulado que exporta funcionalidad específica para que otros archivos la importen y reutilicen.

En la práctica vas a trabajar con dos sistemas de módulos y con dos orígenes distintos: módulos nativos del propio Node y módulos de terceros publicados en npm .

## ¿Cuál es la diferencia entre CommonJS y ES Modules?

Node.js soporta dos sistemas para declarar e importar módulos, y conocer ambos es clave porque vas a encontrarte proyectos con cualquiera de los dos.

## CommonJS, el sistema histórico de Node

CommonJS nació con los inicios de Node.js y sigue presente en muchísimos proyectos. Sus señas de identidad son:

- Sintaxis con `require` para importar y `module.exports` para exportar.
- Extensión de archivo `.js`.
- Ejecución **síncrona**.
- Sistema predeterminado desde el lanzamiento de Node.js.

## ES Modules, la sintaxis moderna

Con ECMAScript 6+ llegó una sintaxis más limpia que hoy es la más utilizada. Sus características:

- Sintaxis con `import` y `export`.
- Extensión `.mjs` para indicar explícitamente que es un módulo.
- Ejecución **asíncrona** por diseño.
- Disponible de forma experimental desde Node.js 12 y estable desde la versión 14 .

> **¿CommonJS o ES Modules, cuál debo usar?** Si tu proyecto corre en Node.js 18 o superior, empieza con ES Modules (`import`/`export`). Si trabajas sobre un proyecto antiguo con `require`, mantén CommonJS y no mezcles ambos en el mismo archivo.

## ¿Qué tipos de módulos puedes usar en Node.js?

Más allá del sistema, los módulos se clasifican por su origen y eso define cómo los traes a tu programa.

## Módulos nativos integrados

Vienen con Node.js de fábrica y resuelven tareas comunes del entorno. Algunos que vas a usar seguido:

- `fs` para manejar el _file system_.
- `http` para crear servicios HTTP.
- `path` para trabajar con rutas de archivos.
- `os` para acceder a información del sistema operativo.

## Módulos de terceros desde npm

Viven en npm, el repositorio público de paquetes, y los traes a tu proyecto con el comando `npm install` seguido del nombre del paquete. Al instalarlos aparecen dentro de la carpeta `node_modules`, que normalmente se ignora del control de versiones .

## ¿Cómo crear y exportar un módulo con CommonJS?

El flujo clásico se resume en exportar funciones desde un archivo y consumirlas desde otro con `require`.

En un archivo `math.js` defines la lógica y la expones:

js function add(a, b) { return a + b; }

function subtract(a, b) { return a - b; }

module.exports = { add, subtract };

Luego, desde `main.js`, lo consumes así:

js const math = require('./math');

console.log(`Suma: ${math.add(5, 3)}`); console.log(`Resta: ${math.subtract(5, 3)}`);

Ejecutas con `node src/main.js` y obtienes los resultados en consola .

## ¿Cómo trabajar con import y export en ES Modules?

El mismo ejemplo con la sintaxis moderna cambia tanto la extensión como las palabras clave. En `math.mjs` exportas directamente cada función:

js export function multiply(a, b) { return a * b; }

export function divide(a, b) { return a / b; }

Y en `main.mjs` las traes con `import`:

js import { multiply, divide } from './math.mjs';

console.log(`Multiplicación: ${multiply(5, 3)}`); console.log(`División: ${divide(6, 2)}`);

Lo ejecutas con `node src/main.mjs` y la diferencia respecto a CommonJS está en la sintaxis y en que la carga es asíncrona por diseño .

## ¿Cómo usar módulos nativos como fs?

Los módulos nativos no requieren instalación. Para leer un archivo `example.txt` con el contenido `Hello, World!`, creas `native.js`:

js const fs = require('fs');

const data = fs.readFileSync('example.txt', 'utf8'); console.log('fileContent:', data);

Aquí `readFileSync` lee el archivo de forma síncrona y `utf8` es la codificación que devuelve el contenido como texto legible .

## ¿Cómo instalar y usar un módulo de terceros desde npm?

Para consumir un paquete externo, primero lo instalas con npm. Por ejemplo, instalas `is-odd` y luego lo usas en `thirdparty.js`:

js const isOdd = require('is-odd');

console.log(isOdd(1)); console.log(isOdd(3));

Al ejecutar el archivo, ya estás aprovechando código que otra persona publicó y mantienes en tu proyecto vía `node_modules`. Recuerda ignorar esa carpeta del repositorio.