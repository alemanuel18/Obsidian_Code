## ¿Cómo se crea un nuevo proyecto en Vue?

Crear un proyecto en Vue puede parecer desafiante a primera vista, pero con las herramientas adecuadas y una guía clara, resulta ser un proceso muy sencillo. Para arrancar con un proyecto en Vue, necesitas tener instalados en tu computadora Node.js, un terminal de comandos y un editor de código que te acomode, como Visual Studio Code. Además, es fundamental que poseas conocimientos básicos en HTML, CSS y JavaScript.

A continuación, te muestro paso a paso cómo lograrlo:

### ¿Qué comando usas para crear el proyecto?

Para iniciar el proyecto de Vue, utiliza el comando `create-vue`. Este se ejecuta a través de `npm` y se recomienda ejecutarlo con la etiqueta `@latest` para asegurar que estás usando la versión más actualizada de Vue.

```bash
npm create vue@latest
```

Este comando iniciará un asistente que te hará algunas preguntas. Asegúrate de responder de la siguiente manera para este ejemplo:

- Nombre del proyecto: `Vue counter game`
- TypeScript: No
- JSX Support: No
- Vue Router: No
- Pinia (estado global): No
- Vitest para Unit Testing: No
- End to End Testing: No
- ESLint para calidad de código: Sí
- Prettier para formateo de código: Sí

### ¿Cómo gestionar las dependencias?

Una vez completado el asistente, el siguiente paso es instalar todas las dependencias necesarias para tu proyecto. Esto puede tomar unos minutos. Dirígete a la carpeta de tu proyecto (en este caso `Vue counter game`) y ejecuta:

```bash
npm install
```

Este comando instalará todos los paquetes necesarios definidos en el archivo `package.json` del proyecto, permitiendo que tu aplicación funcione correctamente.

## Explorando el proyecto inicial

Al abrir el proyecto en Visual Studio Code, te encontrarás con varias carpetas y archivos esenciales que forman la base de cualquier aplicación de Vue.

### ¿Qué contiene la carpeta 'src'?

La carpeta 'src' es donde se ubica todo el código fuente de tu aplicación. Aquí encontrarás los siguientes archivos clave:

- **`App.vue`**: Contiene el componente principal de la aplicación. Aquí podrás ver cómo Vue organiza el HTML, JavaScript y CSS dentro de un solo archivo.
- **`main.js`**: Es el punto de entrada de la aplicación. Este archivo importa los estilos y el componente App, y arranca la aplicación Vue.

### ¿Cómo configurar el entorno de desarrollo?

Para ejecutar y visualizar tu aplicación, ve a tu terminal y ejecuta:

```bash
npm run dev
```

Este comando lanza un servidor de desarrollo y podrás acceder a tu aplicación en el navegador web en el puerto que se te indique (generalmente es el `5173`).

### ¿Qué archivos se utilizan en la construcción con Vite?

Vite es un moderno constructor de proyectos que Vue utiliza internamente. Su configuración se encuentra en el archivo `vite.config.js`. Este archivo define cómo se debe comportar el servidor de desarrollo y cómo se debe construir la aplicación para producción.

## Trabajando dentro del proyecto

Con el proyecto inicial configurado, estás listo para empezar a modificar la aplicación conforme a tus necesidades. Aquí algunos consejos y recursos fundamentales:

### ¿Qué es el folder público?

En el folder 'public', coloca archivos como imágenes y íconos que necesitarás en tu aplicación. Al momento de compilarse para producción, estos archivos estarán disponibles en el mismo directorio de distribución.

### ¿Cómo personalizar la configuración?

Si deseas cambiar cómo se muestran las configuraciones en `VS Code`, accede a los settings del editor. Allí podrás ajustar la forma en que se visualizan las configuraciones de ESLint y Prettier, conforme a tus preferencias.

Avanzar en Vue te ofrecerá no solo la habilidad para crear aplicaciones web eficientes, sino que también te permitirá experimentar con sus herramientas modernas y entender la filosofía detrás del desarrollo web modular.