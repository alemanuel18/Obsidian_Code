El módulo **fs** de Node.js te permite interactuar con el sistema de archivos de tu computadora directamente desde tu código. Aprenderás a ejecutar un CRUD completo: crear, leer, actualizar y eliminar archivos usando funciones nativas, sin instalar dependencias externas.

Esto es útil cuando construyes scripts que generan logs, guardan transcripciones, exportan datos o manipulan recursos locales antes de enviarlos a otro servicio.

## ¿Qué es el módulo fs y cómo se importa en Node.js?

El módulo _file system_ viene incluido en Node.js, así que no necesitas instalarlo. Solo lo importas con `require` y queda listo para usar .

`const fs = require('fs'); 
`const fileName = 'example.txt';

La constante `fileName` guarda el nombre del archivo que vas a manipular en todo el script. Mantenerlo en una variable evita que repitas el string en cada operación y facilita cambiarlo después.

> **¿Qué significa CRUD en el contexto de archivos?** Es el conjunto de cuatro operaciones básicas: _Create_ (crear), _Read_ (leer), _Update_ (actualizar) y _Delete_ (eliminar). El módulo fs te da una función para cada una.

## ¿Cómo creo y leo un archivo con writeFileSync y readFileSync?

Para crear un archivo usas `fs.writeFileSync`, que recibe el nombre del archivo y el contenido que quieres escribir . Si el archivo no existe, lo crea; si ya existe, lo sobrescribe.

```
// Crear 
fs.writeFileSync(fileName, 'Hola, este es un archivo de ejemplo');
console.log('Archivo creado correctamente');
```

Al ejecutar `node fs.js` en la terminal, verás el archivo `example.txt` aparecer en la raíz de tu proyecto con el contenido que definiste.

Para leerlo, usas `fs.readFileSync` y le pasas dos argumentos: el nombre del archivo y la codificación, que por estándar es **UTF-8** .

```
// Leer 
const content = fs.readFileSync(fileName, 'utf-8'); console.log('File content:', content);
```

Un detalle importante: dentro de `console.log`, separa los argumentos con coma. Si concatenas mal o te falta la coma, Node te lanzará un error indicando la línea exacta. Y como dice el instructor, los errores son tus amigos: te dicen qué revisar.

## ¿Cómo actualizo y elimino archivos sin perder el contenido previo?

Para agregar contenido sin borrar lo que ya existe, usa `fs.appendFileSync`. Esta función abre el archivo y añade texto al final, ideal cuando quieres conservar líneas anteriores.

```
// Actualizar 
fs.appendFileSync(fileName, '\nEsta es una nueva línea\n'); console.log('Archivo actualizado correctamente');
```

El `\n` agrega un salto de línea para que el contenido nuevo no quede pegado al anterior. Sin ese salto, todo se imprime en una sola línea y se vuelve ilegible.

> **¿Por qué no se conserva el contenido entre ejecuciones?** Porque el script corre de arriba hacia abajo cada vez. `writeFileSync` reinicia el archivo en cada ejecución y luego `appendFileSync` agrega la línea. Si quieres conservar estados, comenta o separa las operaciones.

## ¿Cómo elimino un archivo con unlinkSync?

La función `fs.unlinkSync` recibe el nombre del archivo y lo borra del sistema .

```
// Eliminar 
fs.unlinkSync(fileName); 
console.log('Archivo eliminado correctamente');
```

Al ejecutar el script completo, verás cómo el archivo pasa por cada estado: se crea, se lee, se actualiza y finalmente desaparece de tu editor.

## ¿Qué diferencia hay entre las versiones Sync y asíncronas?

Las funciones con sufijo `Sync` bloquean la ejecución hasta que terminan. Son más simples para scripts pequeños y ejemplos didácticos. En proyectos reales con alta concurrencia, conviene usar las versiones asíncronas con callbacks o promesas para no bloquear el _event loop_.

## Conceptos y funciones clave que aparecen en la práctica

- **require('fs')**: importa el módulo nativo de file system .
- **writeFileSync(file, data)**: crea o sobrescribe un archivo con contenido .
- **readFileSync(file, encoding)**: lee el contenido de un archivo en la codificación indicada, normalmente UTF-8 .
- **appendFileSync(file, data)**: agrega contenido al final sin borrar lo anterior .
- **unlinkSync(file)**: elimina el archivo del sistema operativo .
- **UTF-8**: estándar de codificación de caracteres que permite leer texto plano correctamente.
- **CRUD**: acrónimo de las cuatro operaciones básicas sobre datos o archivos.