Cuando empiezas a construir interfaces con React, lo primero que necesitas dominar es el manejo de datos. Y ahí aparece una pregunta clave: ¿qué diferencia hay entre **datos estáticos y datos dinámicos en React**, y cómo se renderiza una lista estática paso a paso? Esta guía te lo muestra con un ejercicio práctico.

## ¿Qué son los datos estáticos y los datos dinámicos?

Antes de tocar código, conviene entender la base. En desarrollo existen dos tipos de datos que vas a manejar todo el tiempo, y cada uno tiene un propósito distinto.

Los **datos estáticos** son aquellos que viven dentro de tu código y solo son de lectura. Piensa en ellos como un libro: lo abres, lo lees, pero no modificas su contenido. Ejemplos típicos son listas de navegación o archivos de configuración.

Los **datos dinámicos**, en cambio, llegan desde una fuente externa, normalmente una API o una librería. Estos sí permiten operaciones como leer, actualizar o eliminar información. Ejemplos comunes son los datos del usuario, el clima o las noticias que cambian a diario.

> **¿Cuál es la diferencia entre datos estáticos y dinámicos?** Los estáticos están escritos directamente en el código y no cambian. Los dinámicos vienen de una API externa y pueden modificarse en tiempo real.

## ¿Cómo crear un proyecto en React con Vite desde cero?

Para el ejercicio necesitas un proyecto limpio. Usa Vite, que es rápido y mínimo.

### Estos son los comandos que vas a correr en orden:

1. `npm create vite@latest my-react-app-data` y elige React con JavaScript.
2. Entra a la carpeta del proyecto y ejecuta `npm install`.
3. Abre el proyecto en Visual Studio Code.
4. Corre `npm run dev` y verifica que el navegador muestre la app.

Con eso ya tienes el entorno listo para empezar a trabajar con tu primer componente.

## ¿Cómo crear un componente con datos estáticos en React?

Dentro de `src` crea una carpeta llamada `Components` y dentro un archivo `StaticComponent.jsx`. La estructura base de cualquier componente funcional en React es la misma: defines una _arrow function_, retornas el JSX y al final exportas el componente con `export default`.

## ¿Cómo declarar el array de datos estáticos?

Dentro del componente vas a declarar una constante `items` con un array de strings. Esa información es la que no se va a modificar.

```jsx 
const StaticComponent = () => { 
	const items = ['manzana', 'banana', 'cereza'];
	return ( 
		<ul> {items.map((item, index) => ( 
		<li key={index}>{item}</li> ))} 
		</ul> 
	); 
};

export default StaticComponent;
```

Fíjate en lo que está pasando: el array `items` contiene tres strings fijos. Para mostrarlos en la interfaz, usas el método `.map()`, que recorre cada elemento y devuelve un `<li>` por cada uno.

## ¿Para qué sirve la prop key en el map de React?

La prop `key` es el identificador único que React necesita para distinguir cada elemento de una lista. Sin ella, React lanza un warning y pierde eficiencia al actualizar el DOM. En este ejemplo se usa el `index` como key, aunque en producción se recomienda un id estable cuando exista.

> **¿Por qué usar .map() en lugar de un for?** Porque `.map()` retorna directamente un array de elementos JSX que React puede renderizar. Es más limpio y se integra naturalmente dentro del return.

## ¿Cómo importar y renderizar el componente en App.jsx?

Una vez tienes el componente listo, toca usarlo. Ve al archivo `App.jsx`, borra el contenido por defecto que trae Vite y deja solo tu componente.

### La importación se ve así:

```jsx 
import StaticComponent from './Components/StaticComponent.jsx';

function App() { return <StaticComponent />; }

export default App;
```

Guarda los cambios, vuelve al navegador y vas a ver tu lista renderizada con manzana, banana y cereza. Esa es tu primera lista de **datos estáticos en React** funcionando.

## ¿Por qué dominar los datos estáticos antes que las APIs?

Porque la lógica de iteración, el uso de `.map()`, las keys y la estructura de componentes son exactamente las mismas que vas a usar después con datos dinámicos. La única diferencia será de dónde llegan los datos.

Cuando entiendes cómo React toma un array y lo convierte en elementos visuales, el salto a consumir una API se vuelve mucho más natural. Ya no estarás aprendiendo dos cosas a la vez: solo cambiarás la fuente de los datos.