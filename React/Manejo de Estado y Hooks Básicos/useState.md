Cuando construyes interfaces en React, necesitas un lugar donde guardar información que cambia: un contador, el texto de un input, si un menú está abierto. Para eso existe el **estado local**, y la herramienta que te permite manejarlo es el hook `useState`. Aquí aprendes cómo declararlo, leerlo y actualizarlo dentro de un componente.

## ¿Qué es el estado local en React y por qué importa?

Piensa en el estado como un conjunto de cajas dentro de tu componente. Cada caja guarda un dato, te deja leerlo, actualizarlo y empezar con un valor inicial. Esa es la base del estado local: información que vive dentro de un componente y que React vigila para volver a pintar la UI cuando cambia.

React también tiene **estado global**, pensado para compartir información entre varios componentes. La diferencia es el alcance: el local se queda en su componente; el global viaja por toda la app.

> **¿Qué es el estado local en React?** Es información que un componente guarda internamente para usarla, mostrarla y actualizarla sin depender de otros componentes.

## ¿Cómo se crea un estado con useState paso a paso?

Primero importas el hook desde React y luego lo invocas dentro del componente. `useState` te devuelve dos cosas: la variable para **leer** el valor y la función para **modificarlo**.

El flujo para montar el proyecto desde cero es directo:

1. Crear la app con `npm create vite@latest` y elegir React + JavaScript.
2. Entrar a la carpeta del proyecto e instalar dependencias con `npm install`.
3. Levantar el servidor con `npm run dev`.
4. Crear una carpeta `components` y dentro un archivo `Counter.jsx`.

### Dentro del componente declaras el estado así:

```jsx 
import { useState } from 'react'
const Counter = () => { const [count, setCount] = useState(0)

return ( <div> <h2>El contador está en {count}</h2> <button onClick={() => setCount(count + 1)}>Incrementar</button> <button onClick={() => setCount(count - 1)}>Decrementar</button> </div> ) }

export default Counter
```

Fíjate en la estructura: `count` es el valor que lees, `setCount` es la función que lo actualiza, y el `0` que pasas a `useState` es el **valor inicial**. Esa tripleta resume cómo funciona el estado local.

## ¿Cómo lees y actualizas el valor en la UI?

Para mostrar el dato en pantalla, lo envuelves entre llaves dentro del JSX: `{count}`. Para cambiarlo, llamas a `setCount` con el nuevo valor. Cada clic dispara una actualización y React vuelve a renderizar el componente con la cifra nueva.

> **¿Cuál es la diferencia entre count y setCount?** `count` te deja leer el valor actual del estado. `setCount` es la función que React te entrega para modificar ese valor y disparar el re render.

## ¿Por qué React vuelve a pintar el componente?

Cada vez que llamas a `setCount`, React detecta que el estado cambió. Empieza en cero, pasa a uno, dos, tres, y el componente se actualiza en automático. No necesitas tocar el DOM a mano: el hook se encarga de sincronizar dato y vista.

## ¿Dónde se usa Counter dentro de la aplicación?

Una vez creado el componente, lo importas en `App.jsx` como cualquier otro elemento y lo renderizas:

```jsx 
import Counter from './components/Counter'

function App() { return <Counter /> }

export default App
```

Al abrir el navegador ves el texto inicial con el contador en cero. Haces clic en _Incrementar_ y sube. Haces clic en _Decrementar_ y baja. Ese ciclo, leer, actualizar y volver a leer, es lo que vas a repetir en cualquier interacción que construyas con React.

## ¿En qué otros casos se usa useState en componentes?

Un contador es la puerta de entrada, pero el mismo patrón aplica para muchos escenarios cotidianos en una interfaz:

- Controlar el valor de un input mientras el usuario escribe.
- Mostrar u ocultar un modal, un menú o un dropdown.
- Cambiar entre tema claro y oscuro.
- Guardar el estado de carga mientras se hace una petición.
- Marcar elementos como seleccionados en una lista.

Cada vez que tu UI necesite recordar algo entre interacciones, ahí entra `useState`.