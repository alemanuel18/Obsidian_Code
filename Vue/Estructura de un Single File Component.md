El **Single File Component** es la pieza central de Vue: un archivo `.vue` donde conviven HTML, CSS y JavaScript en un mismo lugar. Si vienes de la web tradicional, vas a sentirte en casa, porque Vue se apoya en los estándares que ya conoces y solo añade sintaxis extra para darte superpoderes como la reactividad.

## Qué es un Single File Component en Vue

Un Single File Component, o archivo `.vue`, es una convención de Vue que te permite escribir toda la lógica, estructura y estilos de un componente en un solo archivo. Esto significa que dejas de saltar entre múltiples archivos para construir una pieza de interfaz.

Vue mantiene su base en HTML, CSS y JavaScript, así que un `.vue` no te obliga a aprender un lenguaje nuevo: te organiza el código que ya escribes.

> **¿Qué es un Single File Component?** Es un archivo `.vue` que agrupa HTML, CSS y JavaScript de un mismo componente, usando las etiquetas `template`, `style` y `script`.

## Cómo se estructura un archivo .vue

Dentro de cada archivo `.vue` vas a encontrar tres etiquetas que organizan el componente. Cada una cumple un rol específico y juntas dan vida a la pieza de interfaz.

- `template`: contiene los nodos de HTML que se van a renderizar. No es una etiqueta de HTML nativa, pero es esencial en Vue.
- `script`: aloja todo el JavaScript del componente, incluida la lógica de estado y comportamiento.
- `style`: define los estilos CSS aplicados al componente.

Por ejemplo, para un contador de juego puedes crear `GameCounter.vue` dentro de la carpeta `components` y escribir un botón de menos, un `span` con el contador y un botón de más:

```vue 
<template> 
	<button>-</button> 
	<span>0</span> 
	<button>+</button> 
</template>
```

## Por qué necesitas usar setup en script

La etiqueta `script` en Vue puede activarse con el atributo `setup`, y aquí está el detalle que marca la diferencia. Ese atributo le indica al archivo que vas a usar la **Composition API**, que es la forma moderna de trabajar con el ciclo de vida y la reactividad en Vue.

Sin `setup`, Vue no reconoce el archivo como un componente válido cuando intentas importarlo. Si lo quitas, el editor lanza un error y la aplicación deja de mostrar el componente en el navegador.

```vue
<script setup> 
	console.log('componente de juego') 
</script>
```
> **¿Para qué sirve `setup` en Vue?** Activa la Composition API dentro del archivo, permitiendo que el componente use reactividad, referencias y el ciclo de vida moderno de Vue.

## Cómo importar un componente en App.vue

Crear el componente no basta: necesitas registrarlo en algún lugar de la aplicación. El **entry point** de toda app de Vue es `App.vue`, y desde ahí puedes importar tus componentes hijos.

La importación se hace con `import` dentro del bloque `script setup`. Vue te permite usar el alias `@`, que apunta a la carpeta `src`, lo que evita rutas relativas largas.

```vue
<script setup> 
	import GameCounter from '@/components/GameCounter.vue' 
</script>
<template> 
	<GameCounter/> 
</template>
```
Una vez importado, lo usas como una etiqueta más dentro del `template`. Si abres las **dev tools** de Vue en el navegador, verás el nodo `App` y debajo el nodo `GameCounter`, confirmando que el componente vive dentro del árbol de la aplicación.

## Cómo correr la aplicación de Vue

Para ver el componente funcionando necesitas levantar el servidor de desarrollo desde la terminal. El comando estándar en proyectos de Vue creados con Vite es directo y rápido.

- Abre la terminal en la raíz del proyecto.
- Ejecuta `npm run dev`.
- Abre el navegador en la URL que te indica la consola.

Después de eso, cualquier `console.log` que hayas escrito en el `script` aparece en la pestaña de info del explorador, lo que te ayuda a verificar que el componente se está ejecutando correctamente.

## Por qué Vue se siente como HTML, CSS y JavaScript

La filosofía de Vue es no alejarte de los estándares de la web. Cada Single File Component es, en esencia, una hoja con tres secciones que ya dominas, más una capa de sintaxis extra que habilita reactividad, propiedades, referencias y manejo del ciclo de vida.

Esa cercanía con la web es la razón por la que escribir componentes en Vue resulta natural: trabajas con `button`, `span`, selectores CSS y sentencias de JavaScript, mientras Vue se encarga del resto.