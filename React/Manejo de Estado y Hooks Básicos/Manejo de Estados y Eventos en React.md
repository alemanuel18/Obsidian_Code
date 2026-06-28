La gestión de eventos en React es una habilidad fundamental para crear aplicaciones interactivas y dinámicas. A través de los eventos, podemos capturar las acciones del usuario como clics, entradas de texto o movimientos del ratón, y responder a ellas de manera eficiente. React simplifica este proceso con su sistema de eventos sintéticos, permitiéndonos crear interfaces de usuario altamente responsivas con un código limpio y mantenible.

## ¿Qué son los eventos sintéticos en React?

Los eventos en React funcionan de manera similar a los eventos nativos de HTML, pero con algunas diferencias importantes. React implementa un sistema de **eventos sintéticos** que actúan como una capa de abstracción sobre los eventos nativos del navegador.

Una diferencia notable es la sintaxis: mientras que en HTML utilizamos nombres de eventos en minúsculas como `onclick`, en React empleamos **camelCase**, escribiendo `onClick`. Esta convención de nomenclatura es característica de React y se aplica a todos los eventos que manejamos.

Otra diferencia fundamental es que en React no pasamos strings a los manejadores de eventos, sino **funciones**. Esto nos permite ejecutar código más complejo y manipular el estado de nuestros componentes cuando ocurre un evento.

```jsx
// HTML tradicional
<button onclick="handleClick()">Clic aquí</button>

// React
<button onClick={handleClick}>Clic aquí</button>
```

## ¿Cómo crear un formulario interactivo con eventos?

Vamos a crear un componente que capture la entrada de texto de un usuario y muestre un saludo personalizado en tiempo real. Este ejemplo ilustra perfectamente cómo los eventos y el estado trabajan juntos en React.

### Creando el componente NameForm

Primero, necesitamos importar el hook `useState` para manejar el estado del componente:

```jsx
import React, { useState } from 'react';

const NameForm = () => {
  const [name, setName] = useState('');
  
  return (
    <div>
      <input 
        type="text" 
        placeholder="Ingresa tu nombre" 
        value={name} 
        onChange={(event) => setName(event.target.value)} 
      />
      <p>Hola, {name ? name : 'visitante'}</p>
    </div>
  );
};

export default NameForm;
```

En este componente:

1. Creamos un **estado** llamado `name` inicializado como un string vacío
2. Utilizamos el evento `onChange` para detectar cuando el usuario escribe en el input
3. Actualizamos el estado `name` con el valor actual del input
4. Mostramos un saludo personalizado, usando un operador ternario para mostrar "visitante" cuando no hay nombre

### Mejorando la experiencia de usuario

Para mejorar la experiencia, podemos agregar un título y estructurar mejor nuestro componente:

```jsx
const NameForm = () => {
  const [name, setName] = useState('');
  
  return (
    <div>
      <h1>Formulario de nombre</h1>
      <input 
        type="text" 
        placeholder="Ingresa tu nombre" 
        value={name} 
        onChange={(event) => setName(event.target.value)} 
      />
      <p>Hola, {name ? name : 'visitante'}</p>
    </div>
  );
};
```

Este patrón de diseño es muy común en React: **capturar eventos del usuario**, **actualizar el estado** y **reflejar esos cambios en la interfaz** de manera inmediata.

## ¿Qué otros eventos podemos manejar en React?

React soporta una amplia variedad de eventos que podemos utilizar para crear interfaces interactivas:

- **Eventos de ratón**: `onClick`, `onMouseOver`, `onMouseOut`
- **Eventos de formulario**: `onChange`, `onSubmit`, `onFocus`, `onBlur`
- **Eventos de teclado**: `onKeyDown`, `onKeyPress`, `onKeyUp`
- **Eventos de clipboard**: `onCopy`, `onCut`, `onPaste`

Todos estos eventos siguen la misma sintaxis con camelCase y reciben funciones como manejadores.

### Ejemplo de un evento onClick

En clases anteriores vimos cómo implementar un botón toggle utilizando el evento `onClick`:

```jsx
const ToggleButton = () => {
  const [isOn, setIsOn] = useState(false);
  
  return (
    <button onClick={() => setIsOn(!isOn)}>
      {isOn ? 'ON' : 'OFF'}
    </button>
  );
};
```

Este componente cambia entre los estados "ON" y "OFF" cada vez que el usuario hace clic en el botón, demostrando cómo podemos usar eventos para crear componentes interactivos.

Los eventos en React nos permiten crear aplicaciones verdaderamente interactivas, respondiendo a las acciones del usuario de manera eficiente y predecible. La combinación de eventos sintéticos y el sistema de estado de React proporciona una forma poderosa de construir interfaces de usuario dinámicas con un código limpio y mantenible.