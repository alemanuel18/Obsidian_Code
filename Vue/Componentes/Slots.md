Los _slots_ en Vue te permiten crear componentes flexibles que actúan como contenedores reutilizables, donde puedes inyectar contenido dinámico desde el componente padre. Si trabajas con Vue, dominar _slots_ y _named slots_ te ayudará a construir layouts y composiciones más limpias, sin duplicar lógica ni estilos.

Esta guía te muestra cómo declararlos, cuándo usar cada tipo y cómo validar si un _slot_ fue recibido usando `useSlots`.

## ¿Qué es un slot en Vue y para qué sirve?

Un _slot_ es un espacio vacío dentro de un componente, una especie de _placeholder_ o _boilerplate_, donde colocas piezas de código u otros componentes. Piensa en él como un hueco reservado que el componente padre rellena con lo que necesite.

> **¿Qué es un slot en Vue?** Es una etiqueta `<slot />` que define dónde se renderizará el contenido hijo que envuelve a un componente. Funciona como un contenedor flexible para reutilizar estructuras visuales.

En el proyecto de ejemplo existe un componente `GameLayout` que debe envolver todas las _cards_ del juego. Sin _slot_, las _cards_ se renderizan fuera del _layout_ y pierden estilos como el `display: grid` con `gap: 2rem` definido en el componente.

## ¿Cómo se declara un slot por defecto?

Se declara con la etiqueta `<slot />` dentro del _template_ del componente. Todo lo que pongas como hijo de ese componente al usarlo se renderizará justo donde está esa etiqueta.

```vue
<!-- GameLayout.vue --> 
<template> 
	<div class="game-layout"> 
		<slot /> 
	</div> 
</template>
```

Luego, en el componente padre, importas y envuelves el contenido:

```vue
<script setup> 
import GameLayout from './GameLayout.vue' 
</script> 

<template> 
	<GameLayout> 
		<GameCard v-for="game in games" :key="game.id" :game="game" /> 
	</GameLayout> 
</template>
```

Un detalle importante: si el _layout_ no aplica los estilos como esperas, revisa propiedades como `max-width`. En el proyecto se ajustó a `90%` para alinear correctamente las _cards_.

## ¿Cómo funcionan los named slots y cuándo usarlos?

El _slot_ genérico siempre renderiza el contenido en el mismo lugar. Pero cuando necesitas pasar varios bloques opcionales, como un título personalizado, un _header_ o un _footer_, los _named slots_ te dan ese control.

Para declarar un _named slot_ dentro del componente, usas el atributo `name`:

```vue
<!-- GameLayout.vue --> 
<template> 
	<div class="game-layout"> 
		<slot name="title" /> 
		<slot /> 
	</div> 
</template>
```
Y en el padre, usas la sintaxis `<template #nombre>` para apuntar a ese _slot_ específico:

```vue 
<GameLayout> 
	<template #title> 
		<h3>Juegos actualizados</h3> 
	</template>
	<GameCard v-for="game in games" :key="game.id" :game="game" /> 
</GameLayout>
```

> **¿Cuál es la diferencia entre slot por defecto y named slot?** El _slot_ por defecto recibe todo el contenido sin nombre y suele usarse como _wrapper_. El _named slot_ recibe contenido específico marcado con `#nombre`, ideal para _headers_, _footers_ o títulos opcionales.

Un detalle clave: la etiqueta `<slot>` no debe ir dentro de un `<template>` cuando la declaras en el componente hijo. Va directamente en el _markup_. Si la envuelves en `<template>`, no se renderiza.

## ¿Cómo detectar si un slot fue pasado con useSlots?

Vue ofrece el _composable_ `useSlots`, que te devuelve un objeto con todos los _slots_ recibidos. Así puedes condicionar qué renderizar según lo que el padre haya enviado.

```vue
<script setup> 
	import { useSlots } from 'vue' 
	const slots = useSlots() console.log(slots) // { title: fn, default: fn } 
</script> 
<template> 
	<h2 v-if="slots.title === undefined">
		Recent Games
	</h2> 
	<slot name="title" /> 
	<slot /> 
</template>
```

Cada propiedad del objeto `slots` es una función, porque representa un componente de Vue. Si el _slot_ no fue enviado, su valor es `undefined`. Con un simple `v-if` decides si mostrar un valor por defecto, como `Recent Games`, o el contenido custom enviado por el padre.

## ¿Cuándo conviene usar cada tipo de slot?

La elección entre uno u otro depende del nivel de personalización que necesites en tu componente.

- Usa el **slot por defecto** cuando quieras crear un _wrapper_ que envuelva una serie de componentes hijos sin diferenciarlos. Es la opción más sencilla para _layouts_ generales.
- Usa **named slots** cuando tu componente tenga zonas específicas como _header_, _footer_, título o _sidebar_, y quieras cambiarlas según la lógica del padre.
- Combina ambos cuando un _layout_ necesite tanto un área principal flexible como secciones nombradas opcionales.

Los _slots_ son una pieza fundamental de la composición en Vue, te permiten construir componentes verdaderamente reutilizables sin acoplarlos a un contenido fijo.