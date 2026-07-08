Manejar eventos en Vue se vuelve sencillo cuando dominas la sintaxis `v-on` y su forma corta con arroba. Aprenderás a iluminar un _search bar_ al hacer focus, a controlar el estado con `ref` y a aplicar clases dinámicas con `computed`, todo dentro de un componente real. Es contenido pensado para quienes ya escriben Vue 3 con Composition API y quieren reforzar interactividad.

## ¿Cómo se escuchan eventos en Vue 3?

En Vue, los eventos del DOM como `focus`, `blur`, `click` o `keydown` se enlazan con la directiva `v-on`, que normalmente escribes con su atajo: el símbolo arroba. Es la alternativa nativa al clásico `addEventListener` que usarías en JavaScript vanilla.

Dentro del componente `SharedSearch`, el ejercicio parte de un `div` con clase `search` que envuelve un `input`. La meta es que al enfocar ese input, el contenedor padre se ilumine. Para empezar, basta con probar el binding así:

```vue 
<input @focus="console.log('onFocus')" @blur="console.log('onBlur')" />
```

Al recargar el proyecto, hacer click sobre el input dispara `onFocus`, y al salir se dispara `onBlur`. Esa es la base sobre la que se construye toda la interacción.

> **¿Qué hace v-on en Vue?** Conecta un evento del DOM con una función o expresión de tu componente. Su forma corta es `@evento`, y reemplaza la necesidad de registrar manualmente un _event listener_.

## ¿Cómo cambiar una clase al hacer focus en un input?

La estrategia es guardar el estado del foco en una variable reactiva y derivar de ahí la clase CSS. Para eso necesitas importar `ref` desde Vue y crear un estado booleano que arranque en `false`.

```js 
import { ref, computed } from 'vue'

const isActive = ref(false)

const onFocus = () => { 
	isActive.value = true 
} 
const onBlur = () => { 
	isActive.value = false 
}

const searchClasses = computed(() => ({ 
	searchActive: isActive.value 
}))
```

Nota el detalle: dentro del `<script setup>` siempre accedes al valor reactivo con `.value`. Olvidarlo es uno de los errores más comunes al empezar con la Composition API.

## ¿Dónde se aplican los eventos y la clase?

Los eventos `@focus` y `@blur` viven en el `input`, porque es el elemento que realmente recibe el cursor. La clase, en cambio, se aplica al `div` padre, que es la cajita que queremos iluminar.

```vue 
<template>
	<div class="search" :class="searchClasses"> 
		<input @focus="onFocus" @blur="onBlur" />
	</div>
</template>
```

Al recargar, el contenedor cambia de estilo cuando el input está activo y vuelve a su estado normal al perder el foco. La clase `searchActive` ya tenía los estilos preparados desde antes.

## ¿Qué cuidados debo tener al usar eventos en Vue?

Los eventos son poderosos, pero también pueden provocar problemas de rendimiento si los atas a estados que mutan con demasiada frecuencia. Cada cambio de estado dispara un _render_ del componente, así que conviene pensar bien dónde colocas la lógica.

Algunos puntos a vigilar:

- Eventos como `onChange` o `onKeyDown` se disparan muchas veces seguidas y pueden generar _side effects_ indeseados.
- `focus` y `blur` son más controlados, pero igual conviene mantener su lógica simple.
- Evita mutar estados pesados o lanzar peticiones dentro de eventos que se repiten constantemente.

> **¿Por qué Vue es mejor que addEventListener?** Porque limpia automáticamente los listeners cuando el componente se desmonta y unifica la sintaxis dentro del template, lo que reduce errores de memoria y código repetido.

## ¿Qué son los modificadores de eventos?

Los modificadores son sufijos que cambian el comportamiento de un evento sin que tengas que escribir lógica extra. El caso más típico es `@submit.prevent`, que evita que un formulario recargue la página al enviarse, equivalente a llamar `event.preventDefault()` manualmente.

Otros modificadores útiles atacan la propagación de eventos, también conocida como _bubbling_, esa cadena en la que un evento sube de hijo a padre como si reventaran burbujas. Con `.stop` detienes esa propagación en seco.

Entre los más usados están:

- `.prevent` para cancelar el comportamiento por defecto del navegador.
- `.stop` para frenar la propagación hacia elementos padres.
- `.once` para que el evento se dispare una sola vez.
- `.self` para que solo reaccione si el evento ocurre en el elemento exacto.

Te recomiendo revisar la documentación oficial de Vue sobre modificadores y aplicarlos al componente que acabamos de construir.