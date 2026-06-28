Vue.js es un framework progresivo para construir interfaces de usuario. En esta clase, exploraremos cómo Vue funciona en el navegador paso a paso, explicando los archivos clave de un proyecto: `index.html`, `main.js` y `App.vue`. También abordaremos conceptos fundamentales como el Virtual DOM y el montaje de un componente.

## La Base: `index.html`

El archivo `index.html` es el punto de entrada de nuestra aplicación. Es un documento HTML simple que incluye un contenedor donde Vue montará la aplicación.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Aplicación Vue</title>
</head>
<body>
    <div id="app"></div>
    <script src="/main.js"></script>
</body>
</html>
```

- El `div` con `id="app"` es donde Vue renderizará nuestra aplicación.
- `main.js` se encarga de inicializar Vue y montar la aplicación en `#app`.

## El Punto de Entrada: `main.js`

El archivo `main.js` es el punto central de la aplicación donde se crea la instancia de Vue y se monta en el DOM.

```js
import { createApp } from 'vue';
import App from './App.vue';

createApp(App).mount('#app');
```

- `import { createApp } from 'vue';` importa la función necesaria para crear una aplicación Vue.
- `import App from './App.vue';` importa el componente raíz.
- `createApp(App).mount('#app');` crea la aplicación y la monta en el elemento `#app` del navegador.

## El Componente Principal: `App.vue`

Vue usa un enfoque basado en componentes. `App.vue` es el componente raíz de la aplicación.

```jsx
<template>
  <div>
    <h1>¡Hola, Vue!</h1>
  </div>
</template>

<script setup>
// Lógica del componente
</script>

<style>
h1 {
  color: blue;
}
</style>
```

- **`<template>`**: Define la estructura HTML del componente.
- **`<script setup>`**: Contiene la lógica del componente. En Vue 3 se usa `setup` para la Composition API, lo verémos después 😉.
- **`<style>`**: Contiene los estilos específicos del componente.

## ¿Qué Sucede en el Navegador?

### Cuando el navegador carga la página:

1. `index.html` carga `main.js`.
2. `main.js` inicializa Vue y monta el componente `App.vue` dentro de `#app`.
3. Vue renderiza el contenido de `App.vue` dentro del `div id="app"`.

Todo esto sucede en algo llamado **“Virtual DOM”**. El **Virtual DOM** es una representación optimizada del DOM real. En lugar de modificar directamente el DOM (lo cual es costoso en rendimiento).

Vue trabaja con una versión virtual que compara cambios y actualiza solo lo necesario. Esto hace que la renderización sea más eficiente.

Cada archivo con terminación `.vue` se le considera un **Single File Component.** Cada archivo que existe con esta terminación Vue lo procesa de la siguiente forma:

1. Crea una instancia del componente.
2. Renderiza (Dibuja en el navegador) su contenido usando el Virtual DOM.
3. Lo inserta en el DOM real dentro del elemento especificado (`#app`).

Una vez termina este proceso se dice que el componente ha sido **montado.**

Vue simplifica el desarrollo de aplicaciones web mediante su sistema basado en componentes y el uso del Virtual DOM para optimizar actualizaciones.

Ahora que entiendes cómo Vue se monta en el navegador, estás listo para profundizar más en su ecosistema y crear aplicaciones interactivas.