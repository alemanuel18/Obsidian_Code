Aprende a usar npm con confianza: desde qué es y cómo te ahorra tiempo, hasta inicializar un proyecto, instalar dependencias, ignorar node_modules y crear scripts en package.json. Con ejemplos claros en Node.js, verás cómo pasar de cero a ejecutar tu primer paquete en minutos.

## ¿Qué es npm y por qué acelera tus proyectos?

Npm es **Node Package Manager**: permite instalar, desinstalar y administrar **paquetes** creados por la comunidad. Con esto, puedes **evitar reinventar la rueda** y reutilizar soluciones mantenidas por miles de personas.

## ¿Qué hace npm en Node.js?

- Gestiona **dependencias** para tus proyectos de JavaScript y Node.js.
- Centraliza configuraciones en **package.json**.
- Facilita compartir código como **paquetes** públicos.
- La mayoría de los paquetes son _open source_: puedes leer y aprender del código.

## ¿Dónde buscar paquetes en npmjs.com?

- Visita npmjs.com para encontrar librerías para React, JavaScript o Node.
- Ejemplo real: el paquete isNumber reporta **cien mil descargas** en una semana. Señal de uso activo.

## ¿Cómo verificar versiones de node y npm?

- Al instalar Node, npm viene incluido.
- Verifica versiones en la terminal:

`node -v npm -v`

## ¿Cómo iniciar un proyecto y configurar package.json?

Inicia un proyecto con **npm init** dentro de la carpeta de trabajo. Responderás preguntas para definir nombre, versión, descripción, _entry point_ y licencia. Esto crea **package.json**, el archivo que describe tu proyecto.

## ¿Qué preguntas hace npm init?

- name: nombre del paquete o proyecto.
- version: por defecto 1.0.0.
- description: por ejemplo, _A Node.js package_.
- entry point: archivo principal, como **main.js** o **index.js**.
- test command, repository y keywords: opcionales.
- author: tu nombre y correo.
- license: **MIT** es una opción común y flexible.

`npm init`

## ¿Qué rol cumple la licencia MIT?

- Permite usar el código en productos comerciales o comunitarios.
- Es ampliamente adoptada por frameworks y librerías.

## ¿Cómo definir el entry point con main.js?

- Crea el archivo que elegiste en npm init, por ejemplo **main.js**.
- Podrás ejecutar tu aplicación con Node o desde un **script** en package.json.

## ¿Cómo instalar dependencias y ejecutar scripts con npm?

Instala paquetes con npm, observa cómo se registran como **dependencies**, y aprende a ejecutar tu código con **scripts**. Además, evita subir node_modules a tu repositorio con un **.gitignore**.

## ¿Cómo instalar isNumber y qué genera npm?

- Instala el paquete desde la terminal:

`npm i isNumber`

- Cambios visibles:
    - Se agrega isNumber a dependencies en package.json.
    - Se crea la carpeta **node_modules** con el código del paquete.
    - Se genera un archivo de bloqueo de dependencias.

## ¿Por qué ignorar node_modules con .gitignore y git init?

- node_modules contiene muchos archivos que no necesitas versionar.
- Crea un **.gitignore** para ignorarlo y luego inicializa Git:

`echo "node_modules/" >> .gitignore git init`

- Beneficio: tu repositorio se mantiene limpio y ligero.

## ¿Cómo usar isNumber en main.js y crear un script start?

- Código de ejemplo en **main.js**:

`const isNumber = require('isNumber'); console.log(isNumber(10));    // true console.log(isNumber('hola'));// false`

- Ejecución directa con Node:

`node main.js`

- Agrega un **script** en package.json para simplificar la ejecución:

`{   "scripts": {     "start": "node main.js"   } }`

- Ahora ejecuta con npm:

`npm run start`

Habilidades y conceptos trabajados: instalación y verificación de **Node y npm**, uso de **npm init**, edición de **package.json**, instalación de **dependencias**, lectura de código en **node_modules**, creación de **.gitignore**, inicialización de **Git**, y ejecución con **scripts**. Si usas Visual Studio Code, puedes apoyarte en herramientas como **GitHub Copilot** para acelerar tu flujo.