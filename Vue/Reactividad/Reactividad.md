La reactividad en Vue es la capacidad de mutar el DOM sin renderizar toda la página, y se logra declarando estados que actúan como el alma de cada componente. Si estás aprendiendo Vue.js y quieres construir interfaces interactivas, dominar `ref` es el primer paso para que tus contadores, formularios y listas cobren vida.

## Qué es la reactividad en Vue y por qué importa

La reactividad permite que un componente actualice únicamente los nodos HTML que cambian, en lugar de volver a pintar toda la aplicación. Esto evita renders costosos y hace que tu interfaz responda al instante cuando un valor cambia.

Dentro de un componente Vue, declaras un _estado_: información interna que puede mutar mientras la aplicación está activa. Cuando ese estado cambia, Vue se encarga de reflejarlo en el DOM solo donde es necesario.

> **¿Qué es un estado en Vue?** Es una variable reactiva que vive dentro de un componente y, al cambiar de valor, actualiza automáticamente las partes del template enlazadas a ella.

## Cómo declarar un estado reactivo con ref en Vue

La API `ref` es la forma más común de crear reactividad en Vue . Existen otras como `reactive` o las propiedades computadas, pero `ref` resuelve la mayoría de los casos cuando empiezas.

### El flujo es directo:

1. Importa `ref` desde Vue con `import { ref } from 'vue'`.
2. Declara una variable, por ejemplo `const counter = ref(0)`, pasando el valor inicial dentro de los paréntesis.
3. Usa esa variable en el template interpolándola con dobles llaves.

Si no le das un valor inicial, el estado queda _undefined_ y no se mostrará nada en pantalla. Por eso siempre conviene inicializarlo, ya sea con un número, un string, un objeto o un arreglo. Cualquier tipo de dato de JavaScript es válido dentro de un `ref`.

## Por qué necesitas usar .value al modificar un ref

Un `ref` no es una variable común; piénsalo como una cajita o _wrapper_ que envuelve el valor real. Para acceder o modificar ese valor desde JavaScript, debes escribir `counter.value` .

### Por ejemplo, una función `increment` se vería así:

```js 
const increment = () => { counter.value++ }

const decrement = () => { counter.value-- }
```

La única excepción es cuando usas el estado directamente en el template de Vue: ahí no necesitas `.value`, Vue lo desempaqueta por ti.

> **¿Cuándo uso .value en un ref?** Siempre que leas o modifiques el estado desde el bloque `<script>`. En el template, Vue lo resuelve automáticamente.

### Cómo enlazar eventos con la directiva v-on en Vue

Para que tu contador reaccione a clics, necesitas conectar tus funciones a eventos del DOM. Vue ofrece la directiva `v-on`, que permite escuchar eventos como `click`, `focus` o `change` .

La sintaxis larga es `v-on:click="increment"`, pero Vue tiene un _shortcut_ mucho más limpio: el símbolo `@`. Así, tu botón quedaría:

```html 
<button @click="decrement">-</button> 
<button @click="increment">+</button>
```

Con esto, cada vez que hagas clic, la función correspondiente actualiza el `.value` del estado y Vue muta solo el nodo HTML donde se interpola el contador. Los botones no se vuelven a pintar; únicamente cambia el número en pantalla.

## Qué pasa cuando recargas la página

Aquí viene un detalle clave: los estados nacen en el momento en que son llamados, pero no perpetúan al recargar la aplicación. Si refrescas el navegador, el contador vuelve a su valor inicial.

Para conservar información entre sesiones se usan APIs del navegador como _local storage_ o _IndexedDB_. Eso sí, ten cuidado con lo que almacenas: guardar datos sensibles ahí puede romper normativas internacionales de protección de datos. No lo hagas.

## Buenas prácticas al trabajar con estados reactivos

Algunos puntos que conviene recordar mientras experimentas con `ref`:

- Inicializa siempre tus estados con un valor por defecto para evitar _undefined_.
- Usa `.value` solo dentro del `<script>`, nunca en el template.
- Aprovecha el _shortcut_ `@` en lugar de `v-on:` para mantener el código legible.
- Reserva `local storage` o `IndexedDB` para datos no sensibles cuando necesites perpetuar el estado.

La reactividad es la base de cualquier aplicación web moderna construida con Vue o React. Una vez la entiendes, puedes construir desde un contador simple hasta dashboards complejos sin preocuparte por manipular el DOM manualmente.