## ¿Qué son los contextos de ejecución y la cadena de alcances?

Los contextos de ejecución y la cadena de alcances son conceptos fundamentales en JavaScript, ya que determinan cómo y dónde se accede a las variables dentro del código. Al usar las palabras clave `var`, `let`, y `const`, es esencial comprender estas diferencias: el tipo de `scope` y el comportamiento de `hoisting`. Esto nos ayudará a tomar decisiones informadas sobre cuándo y cómo utilizar cada una.

![[Pasted image 20260610153303.png]] 
## ¿Por qué es importante el scope en JavaScript?

El scope es crucial porque determina el alcance y la vida útil de una variable. Con `var`, las variables tienen un scope a nivel de función, mientras que `let` y `const` se limitan al bloque en el que se declaran. Esta distinción es vital para evitar errores y entender cómo se ejecuta el código.

Por ejemplo, consideremos el siguiente código:

![[Pasted image 20260610153323.png]]

Aquí, el `console.log` imprime "smartphone costs 499 and is of brand techCode". Las variables `productName` y `price` dentro de la función sobrescriben las del contexto global, mientras que `brand` se toma desde el exterior debido a la cadena de alcances.

¿Cómo funciona el contexto de ejecución?

En JavaScript, el contexto de ejecución puede pensarse como muñecas rusas: el contexto global es la muñeca más grande y los contextos locales son las más pequeñas dentro de ella.

- **Contexto global**: Incluye todas las variables y código que está por fuera de funciones o bloques.
- **Contextos locales**: Son los bloques definidos, por ejemplo, dentro de una función.

¿Cómo se determina el contexto en un código?

A través del uso de llaves `{ }`, podemos identificar los bloques que delimitan los contextos locales. Todo lo que cae fuera de estos bloques pertenece al contexto global.

![[Pasted image 20260610153339.png]]

En el código anterior:

- `userPoints` y `console.log(evaluatePoints())` forman parte del contexto global.
- `evaluatePoints()` es un contexto local que contiene su propio flujo de ejecución.

¿Qué es el scope chain o cadena de alcances?

La cadena de alcances define cómo JavaScript encuentra las variables. Un contexto local puede acceder a variables en contexto global, pero no al revés. La búsqueda de variables funciona de adentro hacia afuera, asegurándose de que no haya acceso entre contextos locales iguales.

¿Cuándo ocurre el error 'variable no definida'?

Esto ocurre cuando un contexto local busca una variable que no existe ni localmente ni en ningún contexto superior.

![[Pasted image 20260610153353.png]]

En este ejemplo, intentar acceder a `localVariable` y `local3Variable` en contextos que no las definen o que no tienen acceso a ellas desencadena dichos errores.

Comprendiendo los errores de variable no definida

Es importante internalizar la restricción de que los contextos iguales no pueden comunicarse entre sí sin que compartan un contexto padre donde esté definida la variable de interés. Este entendimiento permitirá evitar múltiples errores en implementaciones más complejas, asegurando un manejo eficiente de cómo y dónde se posicionan y utilizan las variables.

Motívate a seguir profundizando en estos conceptos. La práctica y comprensión de cómo JavaScript maneja el scope y los contextos de ejecución te harán un desarrollador más hábil y capaz de escribir código más eficiente y sin errores.