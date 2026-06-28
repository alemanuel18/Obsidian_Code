## ¿Qué son las props en Vue.js?

Las props, o propiedades, son fundamentales en Vue.js y actúan como fragmentos de información, similares a variables, que permiten pasar datos de un componente padre a un componente hijo. Al entender las props, podemos manipular cómo fluyen los datos dentro de las aplicaciones de Vue, garantizando un código más robusto y reutilizable.

En un contexto práctico, considera que tienes un componente root llamado `app` y deseas pasar datos, como variables o estados, al componente hijo `game counter`. Aquí es donde las props juegan un papel crucial.

## ¿Cómo declarar y pasar props en Vue.js?

### Declaración de propiedades en el componente hijo

Para utilizar las props, primero debes declararlas en el componente hijo. Imagina que estás trabajando en un juego donde tienes que adivinar un número dentro de un rango. Comienza declarando constantes para representar el número mínimo (`minNumber`) y el número máximo (`maxNumber`) en el componente `app`:

```javascript
// En App.vue
const minNumber = 0;
const maxNumber = 50;
```

Luego, en el componente `game counter`, utiliza la función `defineProps`, que Vue.js importa globalmente, para definir las props que necesita:

```javascript
// En GameCounter.vue
const { minNumber, maxNumber } = defineProps(['minNumber', 'maxNumber']);
```

### Pasando las props al componente hijo

Para pasar las props desde el componente `app` al `game counter`, se realiza de manera similar a pasar atributos en HTML. Aunque las palabras se escriben en camelCase en JavaScript, Vue.js recomienda usar Kebab case en los atributos HTML:

```html
<!-- En App.vue -->
<game-counter :min-number="minNumber" :max-number="maxNumber"></game-counter>
```

Vue.js simplifica el proceso al permitir el uso de la directiva `v-bind` para vincular las variables de JavaScript a sus respectivos atributos:

```html
<game-counter v-bind:min-number="minNumber" v-bind:max-number="maxNumber"></game-counter>
```

## ¿Cómo validar y usar adecuadamente las props?

### Validación de las props

Una vez que las props están definidas, es importante utilizarlas y validar sus tipos. La validación garantiza que las props sean del tipo correcto, proporcionando una capa adicional de seguridad y previsibilidad al desarrollar aplicaciones Vue.js.

### Uso y explotación de la reactividad

Vue.js es famoso por su capacidad de reactividad. Antes de Vue 3.5, desestructurar las props podía significar perder esta reactividad, lo que provocaba que los componentes hijos no detectaran cambios en las props. Sin embargo, desde Vue 3.5, este problema se ha resuelto.

Escribe un `console.log` para verificar si las props funcionan como esperas:

```javascript
// En GameCounter.vue
console.log(minNumber, maxNumber);
```

### Importancia de mantener la reactividad

Con las mejoras en Vue 3.5, es más fácil asegurarse de que las props mantengan la reactividad. En proyectos con versiones anteriores, debes manejar las props directamente sin desestructurarlas:

```javascript
const props = defineProps();
console.log(props.minNumber, props.maxNumber);
```

Identifica si las propiedades están desactualizadas o si su reactividad está comprometida, y adopta una sólida práctica al definir y usar props, lo cual es clave para desarrollar aplicaciones Vue.js eficientes y efectivas.