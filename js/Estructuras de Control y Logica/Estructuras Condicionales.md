Dominar las **estructuras condicionales** en JavaScript es el primer paso para que tu código tome decisiones de forma inteligente. Cuando ya sabes crear variables, constantes y funciones, el siguiente reto es determinar **qué parte del código se ejecuta** dependiendo de una condición específica. Aquí es donde entran en acción las estructuras de control.

## ¿Qué es la estructura if y cómo funciona?

La palabra reservada **if** significa literalmente "si" en español. Su lógica es directa: **si pasa esto, entonces ejecuta esto** . La sintaxis básica requiere tres elementos:

- La palabra `if` seguida de **paréntesis**.
- Dentro de los paréntesis, una **condición** que se evalúa.
- Dentro de **llaves** (_brackets_), el bloque de código que se ejecuta si la condición es verdadera.

javascript let nombre = "Diego";

if (nombre === "Diego") { console.log("Hola, Diego"); }

En este ejemplo se utiliza el **operador de asignación** (`=`) para darle un valor a la variable `nombre` . Después, dentro del `if`, se emplea el **operador de igualdad estricta** (`===`) para comparar si el valor almacenado coincide con `"Diego"`. Si la condición se cumple, el `console.log` imprime el mensaje en la consola del navegador .

## ¿Qué sucede cuando la condición no se cumple?

Si cambias el valor de la variable a otro nombre, por ejemplo `"Nico"`, la condición `nombre === "Diego"` ya no es verdadera y **no se ejecuta ningún código** . Para manejar ese escenario existe **else**, que actúa como la instrucción _default_: el bloque que se ejecuta cuando ninguna condición previa se cumplió.

javascript let nombre = "Nico";

if (nombre === "Diego") { console.log("Hola, Diego"); } else { console.log("Nombre no encontrado"); }

Es una buena práctica incluir siempre un `else` que ofrezca una **respuesta por defecto**. Así evitas que tu programa quede en silencio cuando los datos no coinciden con lo esperado .

## ¿Cómo agregar múltiples condiciones con else if?

Cuando necesitas evaluar más de un caso, la estructura crece con **else if** . Esto te permite encadenar varias condiciones antes de llegar al bloque _default_.

javascript let nombre = "Nico";

if (nombre === "Diego") { console.log("Hola, Diego"); } else if (nombre === "Nico") { console.log("Hola, Nico"); } else { console.log("Nombre no encontrado"); }

El flujo funciona así:

- Primero evalúa si `nombre` es `"Diego"`.
- Si no lo es, evalúa la segunda condición: si `nombre` es `"Nico"` .
- Si ninguna condición se cumple, ejecuta el bloque `else`.

Un error común es escribir `else if` **sin definir la condición** dentro de los paréntesis. JavaScript lanzará un error indicando la línea exacta del problema . Siempre verifica que cada `else if` contenga una expresión válida entre paréntesis.

## ¿Qué papel juegan los operadores en las condiciones?

Los **operadores** son los símbolos que hacen posible cada validación . En los ejemplos anteriores aparecen dos fundamentales:

- **Operador de asignación** (`=`): asigna un valor a una variable.
- **Operador de igualdad estricta** (`===`): compara tanto el valor como el tipo de dato.

Sin operadores, las estructuras de control no podrían determinar si una condición es verdadera o falsa. Son la pieza que conecta la variable con el valor que deseas comparar.

## ¿Cómo probar tu código en el navegador?

Para verificar los resultados puedes utilizar un **servidor local** desde Visual Studio Code mediante un _plugin_ como _Live Server_ . Al guardar el archivo, los cambios se reflejan automáticamente en la consola del navegador. Abre el **inspector de elementos**, dirígete a la pestaña de consola y ahí verás la salida de cada `console.log` junto con el número de línea correspondiente .

Esta forma de trabajar te permite iterar rápidamente: cambias el valor de la variable, guardas y observas al instante qué bloque de código se ejecutó.

Si quieres practicar, intenta agregar más condiciones con `else if` para saludar a diferentes nombres y comparte en los comentarios cuántas condiciones lograste encadenar.