Trabajar con _refs_ en Vue te permite acceder directamente a un nodo HTML real cuando necesitas invocar métodos nativos del navegador, como reproducir un video automáticamente al abrir un modal. Es un mecanismo pensado para desarrolladores que ya manejan componentes en Vue y quieren ir un paso más allá del estado reactivo.

## ¿Por qué Vue necesita refs si ya existe el Virtual DOM?

Vue, como la mayoría de frameworks reactivos para la web, trabaja con un _Virtual DOM_: una representación en memoria del DOM HTML actual sobre la que se calculan los cambios antes de aplicarlos al navegador. Hacerlo directamente sobre el DOM real sería costoso en rendimiento.

Esa optimización tiene una contraparte. Dentro de la etiqueta `script` de un componente, tú no estás hablando con el DOM real, sino con el ciclo de vida del componente. Por eso no puedes hacer un `querySelector` y llamar a `.play()` como en JavaScript plano .

> **¿Qué es el Virtual DOM en Vue?** Es una copia en memoria del DOM HTML que Vue usa para calcular los cambios de estado antes de aplicarlos. Así evita manipular directamente el navegador, que sería mucho más lento.

## ¿Cómo se declara un ref en Vue para apuntar a un nodo?

La solución que ofrece Vue son los _refs_. Un ref te permite declarar una referencia y enlazarla a un nodo específico del template para acceder a él como elemento HTML real .

El flujo es directo y son tres pasos sencillos:

1. Importar `ref` desde la librería de Vue.
2. Declarar una constante, por ejemplo `const videoRef = ref(null)`, inicializada en `null` porque al inicio de la app el nodo aún no existe.
3. En el template, agregar el atributo `ref` al elemento con el mismo nombre de la variable: `ref="videoRef"`.

El detalle clave es el nombre. Si tu variable se llama `video` pero en el template escribes `ref="videoRef"`, Vue no va a enlazar nada. Tienen que coincidir exactamente, y no necesitas usar `v-bind` ni sintaxis adicional .

## ¿Cómo accedo al nodo HTML desde el ref?

Una vez declarado el ref, el nodo no está disponible inmediatamente. Tienes que esperar a que el componente se monte. Para eso usas el hook `onMounted`, que se ejecuta justo cuando el componente ya está en el DOM real.

Dentro de `onMounted` accedes al nodo a través de `videoRef.value`. Ese `.value` es lo que te entrega el elemento HTML real, no el objeto reactivo de Vue. Si haces `console.log(videoRef.value)` vas a ver el nodo `<video>` tal cual existe en el navegador .

```js 
import { ref, onMounted } from 'vue'

const videoRef = ref(null)

onMounted(() => { videoRef.value.play() })
```

Con `videoRef.value.play()` invocas el método nativo del elemento `<video>` de HTML, y el video arranca solo cuando se abre el modal.

## ¿Para qué sirven los refs en una aplicación real?

Los refs no son la forma habitual de trabajar en Vue. Lo normal es manejar todo a través del estado reactivo y dejar que el framework actualice el DOM por ti. Pero hay escenarios donde necesitas el nodo de carne y hueso.

- Invocar métodos nativos del DOM como `.play()`, `.pause()`, `.focus()` o `.scrollIntoView()`.
- Integrar bibliotecas de terceros que reciben un elemento HTML como argumento para inicializarse.
- Usar APIs del navegador que requieren un nodo específico, como la API de captura de audio, _canvas_ o _intersection observer_.

> **¿Cuándo debo usar un ref en lugar del estado reactivo?** Úsalo solo cuando necesites el elemento HTML real para llamar métodos nativos o pasarlo a una librería externa. Para todo lo demás, el estado reactivo de Vue es más limpio y predecible.

Detrás de toda esta mecánica hay una idea que conviene no perder de vista: **Vue es solamente JavaScript**. Lo mismo aplica para cualquier framework web moderno. Los refs son el puente entre la abstracción reactiva y el JavaScript del navegador que siempre estuvo ahí.

¿Qué casos de uso se te ocurren a ti para usar un _ref_? Capturar la voz de alguien, dibujar en un _canvas_, conectar una API del navegador de forma creativa.