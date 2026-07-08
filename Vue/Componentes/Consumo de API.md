Consumir una API en Vue es tan directo como usar `fetch` de JavaScript, pero la magia aparece cuando combinas la petición con el ciclo de vida del componente y un objeto reactivo que detecta cambios profundos en la respuesta. Aquí aprenderás a clonar un proyecto base desde GitHub, conectar tu API y manejar estados de carga, error y datos con `reactive`.

## Cómo clono el proyecto base desde GitHub para empezar

Antes de escribir código nuevo, necesitas el punto de partida correcto. El proyecto vive en un repositorio y trae todos los componentes listos para que tú solo te enfoques en consumir la API.

La rama clave es `starting-project`. Una vez clonado, te mueves a esa rama con `git checkout starting-project` y abres la carpeta en Visual Studio Code .

Dentro encontrarás una carpeta `components` con piezas pensadas para clonar la página de Game Stream:

- _Card_: muestra la información de cada juego.
- _GameGallery_: presenta la galería completa.
- _GameLayout_: actúa como _wrapper_ que acomoda los elementos.
- _GameModal_: abre el video del juego.
- _GameTags_: renderiza las etiquetas.
- _GameVideoPlayer_: reproduce el video .

Pensar en componentes así, identificando cada bloque visual de la interfaz, es la forma correcta de estructurar una app en Vue.

## Cómo hago la primera petición fetch dentro de App.vue

La petición la haremos desde la raíz de la aplicación, en `App.vue`. La receta es la misma que en JavaScript puro: declaras una constante con la URL de la API y usas `fetch` dentro de una función asíncrona.

```js 
const API_URL = '[https://tu-api/games](https://tu-api/games)'

async function fetchGames() { 
	const response = await fetch(API_URL) 
	const json = await response.json() console.log(json) 
}
```

Como `fetch` y `response.json()` son procesos asíncronos, ambos necesitan `await`. Hasta aquí todo es JavaScript clásico .

> **¿Dónde debo ejecutar la función fetch en Vue?** Dentro del _hook_ `onMounted`, que se dispara cuando el componente ya tiene su HTML y JavaScript renderizados en el navegador. Ese es el momento seguro para pedir datos.

Importas `onMounted` desde `vue` y le pasas un _callback_ que llama a `fetchGames()`. Al guardar y abrir la consola, verás el array de juegos llegando directo desde la API .

## Por qué onMounted debe ser síncrono

Los _hooks_ del ciclo de vida en Vue son síncronos. No puedes pasarle un `async/await` directamente al _callback_ de `onMounted`. Llama a tu función asíncrona desde adentro, pero no conviertas el _hook_ mismo en asíncrono.

## Qué es un objeto reactivo y cuándo conviene usarlo

Una petición sin manejo de errores ni estado de carga está incompleta. Aquí entra `reactive`, la tercera forma de declarar reactividad en Vue, después de `ref` y `computed`.

> **¿Qué es un objeto reactivo en Vue?** Es un objeto creado con `reactive()` que permite detectar cambios de forma profunda en sus propiedades, ideal para manejar respuestas de API, formularios complejos o estructuras anidadas.

La mayor ventaja es la reactividad profunda: si cambia una propiedad en el nivel tres o cuatro de un objeto grande, Vue lo detecta. La contraparte es que tiene un costo de _performance_ mayor y, si desestructuras sus propiedades, pierden la reactividad .

## Cómo declaro state con reactive para manejar carga, error y datos

La convención es agrupar tres propiedades en un solo objeto `state`: el error, el indicador de carga y los datos.

```js 
import { reactive, onMounted } from 'vue'

const state = reactive({ error: null, isLoading: false, data: [] })
```

A diferencia de `ref`, no necesitas usar `.value` para acceder a las propiedades. Escribes `state.data` o `state.error` y listo, sigue siendo reactivo .

## Cómo integro try catch finally con el objeto reactivo

Con el `state` listo, refactorizas `fetchGames` para que actualice cada propiedad según lo que ocurra en la petición.

```js 
async function fetchGames() { 
	state.isLoading = true 
	try { 
		const response = await fetch(API_URL) 
		const json = await response.json() 
		state.data = json 
	} catch (error) { 
		console.error(error) 
		state.error = error 
	} finally { 
		state.isLoading = false 
	} 
}

onMounted(() => { fetchGames() })
```

El bloque `try` asigna los datos cuando la petición es exitosa. El `catch` captura cualquier fallo y lo guarda en `state.error`. Y el `finally` se ejecuta siempre, garantizando que `isLoading` vuelva a `false` sin importar el resultado .

> **¿Cuándo uso reactive en lugar de ref?** Usa `reactive` para objetos o arrays donde necesitas detectar cambios profundos, como respuestas de API. Usa `ref` para valores primitivos como números, strings o booleanos sueltos.

Una advertencia importante: si haces `const { data } = state`, esa variable `data` deja de ser reactiva. Mantén siempre el acceso vía `state.propiedad` para conservar la conexión con Vue.