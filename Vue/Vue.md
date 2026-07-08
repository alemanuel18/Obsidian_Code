Vue.js es un framework progresivo de JavaScript que te permite crear interfaces de usuario dinámicas en cualquier página HTML, sin configuraciones extra. Si ya manejas HTML, CSS y JavaScript, tienes todo lo necesario para empezar a construir componentes reactivos, gráficos interactivos y aplicaciones robustas que se actualizan en tiempo real.

Esto importa para cualquier desarrollador frontend que quiera resolver retos comunes —como una gráfica de barras conectada a un _slider_— con menos código y más claridad.

## Por qué elegir Vue.js para construir interfaces dinámicas

Imagina que tu jefe te pide una gráfica de barras con las ventas de los últimos meses, pero con una vuelta de tuerca: quiere mover un _slider_ y que las barras se ajusten en vivo. Hacer esto con JavaScript puro se vuelve tedioso porque cada elemento tiene que reaccionar al cambio.

Vue resuelve esto con un **Virtual DOM**, una representación en memoria que crea nodos de referencia al DOM real para aplicar cambios rápidamente. Lo instalas con un simple _script_ al final de tu _body_ y listo.

> **¿Qué es Vue.js?** Es un framework progresivo de JavaScript para crear interfaces reactivas en HTML usando directivas, estados y propiedades computadas, sin necesidad de un _build system_ complejo.

## Cómo se instala y monta una aplicación Vue

La instalación es directa: copias el _script_ de Vue y lo pegas cerca del _body_. Luego le asignas un `id="app"` a tu _body_ (o al contenedor que quieras controlar) para que Vue sepa dónde montarse.

Después creas tu aplicación con `createApp`, un método nativo que recibe un objeto con la función `setup`. Dentro de `setup` declaras toda la lógica reactiva que tu página va a usar.

```js 
const { createApp, ref, computed } = Vue
createApp({ setup() { console.log("Hello, world") return {} } }).mount("#app")
```

Finalmente llamas a `.mount("#app")` para enlazar la aplicación con el nodo HTML. Si abres las herramientas de desarrollador y ves el `Hello, world` en la consola, Vue ya está corriendo.

## Cómo conectar lógica de JavaScript con HTML usando referencias

Una de las funciones más potentes de Vue son los **states o references**, que conectan variables de JavaScript directamente con nodos HTML. Para usarlas, declaras la referencia dentro de `setup` y la retornas en un objeto.

Una vez retornada, puedes interpolarla en el HTML con dobles llaves `{{ input }}`. Esa es la sintaxis que Vue usa para mostrar variables dinámicas. Si inicializas el input en cero y mueves el _slider_, verás cómo el valor cambia en pantalla sin escribir un solo _event listener_.

## Qué son las computed properties y cómo iterar con v-for

Las **computed properties** son valores que Vue recalcula automáticamente cada vez que cambia una dependencia. En el caso de la gráfica de barras, cada vez que mueves el _slider_ la propiedad computada recorre los datos, ajusta cada barra y devuelve un nuevo arreglo con `label`, `value` y `height`.

La lógica suele incluir límites: si el valor ajustado es menor a cero, retorna cero; si supera el máximo más 10, se queda en ese tope. Así proteges la visualización de valores extremos.

> **¿Qué hace una computed property en Vue?** Calcula y memoriza un valor derivado de otros estados reactivos. Cuando una dependencia cambia, Vue ejecuta la función de nuevo y actualiza el resultado en pantalla.

## Cómo renderizar listas dinámicas con la directiva v-for

En lugar de declarar cada barra a mano, declaras el componente una sola vez y lo repites con la directiva `v-for`. La sintaxis es `v-for="var in bars"`, donde `bars` es el arreglo reactivo.

### Algunas reglas clave al iterar en Vue:

- Cada elemento iterado necesita una `key` única, normalmente `var.label`.
- Para enlazar atributos dinámicos usas `:` antes del atributo, por ejemplo `:style`.
- Los estilos en línea se pasan como objeto JavaScript, no como string.
- Las variables se interpolan con dobles llaves dentro del HTML.

```html
<div v-for="var in bars" :key="var.label" :style="{ height: var.height + '%' }"> {{ var.value }} <span>{{ var.label }}</span> </div>
```

Con ese cambio, cada vez que mueves el _slider_, todas las barras se redibujan al instante. Ese es el principio de **reactividad**: actualizar la interfaz sin manipular el DOM manualmente.

## Por qué Vue.js es una herramienta versátil para frontend

Lo que viste con la gráfica es apenas una muestra. Vue te permite construir componentes reutilizables, manejar efectos dinámicos y escalar interfaces complejas con código compacto.

### Algunas razones para apostar por Vue:

- Sintaxis basada en atributos y _templates_ HTML, fácil de leer.
- Reactividad incorporada con `ref` y `computed`.
- Directivas como `v-for` que reducen código repetido.
- Documentación clara y una comunidad activa.
- Ecosistema de librerías que cubren _routing_, estado global y más.

---

## 📂 Índice de Contenidos

- [[Vue/Crear un Proyecto de Vue|Crear un Proyecto de Vue]]
- [[Vue/Estructura de un Single File Component|Estructura de un Single File Component]]
- [[Vue/Vue Composition API vs Options API|Vue Composition API vs Options API]]
- [[Vue/Vue en el Navegador|Vue en el Navegador]]
- [[Vue/v-bind|v-bind]]

### Componentes
- [[Vue/Componentes/Ciclos de Vida de un Componente en Vue 3|Ciclos de Vida de un Componente en Vue 3]]
- [[Vue/Componentes/Consumo de API|Consumo de API]]
- [[Vue/Componentes/Herencia|Herencia]]
- [[Vue/Componentes/Pensamiento por componentes|Pensamiento por componentes]]
- [[Vue/Componentes/Reactive vs Ref en Vue 3 ¿Cuál es la diferencia?|Reactive vs Ref en Vue 3 ¿Cuál es la diferencia?]]
- [[Vue/Componentes/Slots|Slots]]
- [[Vue/Componentes/v-for|v-for]]

### Despliegue
- [[Vue/Despliegue/Desplegar en Netlify|Desplegar en Netlify]]
- [[Vue/Despliegue/Despliegue|Despliegue]]
- [[Vue/Despliegue/Despliegue con GitHub actions y pages|Despliegue con GitHub actions y pages]]

### Estilos
- [[Vue/Estilos/Estilos Globales|Estilos Globales]]
- [[Vue/Estilos/Estilos en Vue|Estilos en Vue]]

### Manejo De Eventos E Input
- [[Vue/Manejo de eventos e input/EMIT|EMIT]]
- [[Vue/Manejo de eventos e input/Focus y Blur|Focus y Blur]]
- [[Vue/Manejo de eventos e input/VModel|VModel]]

### Optimizacion
- [[Vue/Optimizacion/Componentes dinámicos con tag|Componentes dinámicos con tag]]
- [[Vue/Optimizacion/Composables|Composables]]
- [[Vue/Optimizacion/Entendiendo el Virtual DOM a profundidad|Entendiendo el Virtual DOM a profundidad]]
- [[Vue/Optimizacion/Modales y manejo de Estados Globales|Modales y manejo de Estados Globales]]
- [[Vue/Optimizacion/Teleport|Teleport]]
- [[Vue/Optimizacion/ref para acceder al DOM real|ref para acceder al DOM real]]

### Props
- [[Vue/Props/Props|Props]]
- [[Vue/Props/Validar Props|Validar Props]]

### Reactividad
- [[Vue/Reactividad/Computed|Computed]]
- [[Vue/Reactividad/Reactividad|Reactividad]]
- [[Vue/Reactividad/Watchers|Watchers]]
- [[Vue/Reactividad/v-if vs v-show|v-if vs v-show]]
- [[Vue/Reactividad/¿Cómo funciona ref en Vue 3?|¿Cómo funciona ref en Vue 3?]]


---

[[Welcome|⬅️ Volver al Hub Principal]]
