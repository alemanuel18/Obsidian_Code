El estado en React tiene dos reglas de oro: nunca lo actualizas directamente y cada cambio dispara un nuevo renderizado del componente. Si entiendes esto, dominas la base de la reactividad en React y puedes construir interfaces dinámicas con confianza.

Para verlo en acción, vamos a crear un _ToggleButton_: un botón que alterna entre dos estados, activo e inactivo, y que actualiza su texto en pantalla con cada clic.

## ¿Por qué no puedes modificar el estado directamente en React?

En React, el estado vive bajo reglas estrictas. Cuando usas `useState`, recibes dos cosas: la variable que guarda el valor y una función _setter_ para actualizarla. Esa función no es opcional, es el único camino válido.

Si en el ejemplo anterior teníamos `count`, no podíamos reasignarlo directamente. Teníamos que pasar por `setCount`. Lo mismo aplica aquí: la variable se lee, el _setter_ se usa para escribir .

> **¿Qué pasa si modifico el estado directamente?** React no detecta el cambio y el componente no se vuelve a renderizar. La interfaz queda desincronizada con tu lógica.

La razón es simple: React necesita saber cuándo algo cambió para volver a pintar el componente. Esa detección ocurre dentro del _setter_, no fuera.

## ¿Cómo se construye un ToggleButton paso a paso?

Empezamos creando un archivo nuevo llamado `ToggleButton.jsx`. Dentro definimos una _arrow function_, la exportamos por defecto e importamos `useState` desde la librería de React .

Un _toggle_ es justamente eso: un componente que alterna entre dos estados. Cero o uno, encendido o apagado, activo o inactivo.

## ¿Cómo declarar el estado con useState?

Declaramos el estado con una convención que vale la pena adoptar:

- El nombre de la variable empieza con `is` cuando manejas booleanos, por ejemplo `isActive`.
- El _setter_ usa el prefijo `set` seguido del nombre de la variable, en este caso `setIsActive`.
- El valor inicial se pasa como argumento a `useState`, aquí `false` porque el botón arranca inactivo.

```jsx 
const [isActive, setIsActive] = useState(false);
```

Esta nomenclatura no es capricho. Cuando alguien lee `isActive`, ya sabe que está frente a un booleano sin necesidad de buscar la declaración .

## ¿Cómo alternar el valor con onClick?

En el `return` colocamos un botón con un evento `onClick`. Dentro del _handler_ llamamos a `setIsActive` y le pasamos el valor opuesto al actual usando el operador de negación:

```jsx 
<button onClick={() => setIsActive(!isActive)}> 
	{isActive ? 'activo' : 'inactivo'} 
</button>
```

El truco está en `!isActive`. Si el valor es `false`, el operador lo convierte en `true`, y viceversa. Pero ojo: este cambio solo funciona porque lo pasamos a través de `setIsActive`. Si intentaras escribir `isActive = !isActive` directamente, React no se entera y nada ocurre en pantalla .

> **¿Por qué usar el prefijo is en variables booleanas?** Porque comunica intención. Quien lea tu código sabe de inmediato que la variable solo puede ser verdadera o falsa, y eso facilita el mantenimiento.

## ¿Cómo renderiza React los cambios de estado?

Dentro del botón usamos un operador ternario para mostrar texto distinto según el valor de `isActive`. Si es `true`, aparece _activo_. Si es `false`, aparece _inactivo_.

Al guardar e importar el componente en `App`, lo vemos en el navegador. Cada clic cambia el texto al instante. Esa velocidad no es magia: React detecta que el estado cambió, marca el componente como obsoleto y vuelve a renderizarlo con el nuevo valor .

Este ciclo, evento, actualización con _setter_, nuevo renderizado, es el corazón de cualquier aplicación en React. Lo entendiste con un botón, pero el mismo patrón aplica para formularios, listas, modales y cualquier interfaz reactiva que construyas.

## ¿Qué reto puedes hacer ahora?

Reemplaza el texto _activo/inactivo_ por algo más visual:

- Un emoji como 🟢 y 🔴.
- Un ícono de una librería como React Icons.
- Un texto personalizado en otro idioma.