Extraer solo una parte de un _array_ sin alterar el original es una operación frecuente en programación. El método **slice** permite hacer exactamente eso: tomar una fracción específica de un _array_ indicando posiciones de inicio y fin, y devolver un nuevo _array_ con esos elementos.

## ¿Cómo funciona slice con un solo parámetro?

Cuando se le pasa **un único argumento**, slice lo interpreta como el **índice de inicio**. A partir de esa posición, devuelve todos los elementos hasta el final del _array_ .

Por ejemplo, con este _array_ de animales:

`const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];`

`console.log(animals.slice(2));` // ['camel', 'duck', 'elephant']

Al pasar `2`, se obtienen los elementos desde la posición dos (camel) hasta el último (elephant).

## ¿Qué sucede cuando se usan dos parámetros en slice?

El segundo parámetro indica el **índice final**, pero ese índice **no se incluye** en el resultado . Es decir, slice extrae desde el inicio hasta una posición antes del valor indicado.

`console.log(animals.slice(2, 4));` // ['camel', 'duck']

- El índice `2` corresponde a "camel".
- El índice `4` corresponde a "elephant", pero **no se incluye**.
- El resultado contiene solo las posiciones 2 y 3.

Si se quiere incluir el elefante, hay que ajustar el segundo parámetro:

`console.log(animals.slice(1, 5));` // ['bison', 'camel', 'duck', 'elephant']

## ¿Se pueden usar índices negativos con slice?

Sí. Los **números negativos** permiten contar desde el final del _array_ hacia atrás . Esto resulta muy útil cuando el _array_ tiene muchos elementos y solo interesan los últimos.

- `-1` representa el último elemento.
- `-2` representa el penúltimo.

`console.log(animals.slice(-2));` // ['duck', 'elephant']

También se pueden **combinar índices positivos y negativos**:

`console.log(animals.slice(2, -1));` // ['camel', 'duck']

Aquí se toma desde la posición 2 hasta la posición `-1` (elephant), que no se incluye.

## ¿Qué pasa si se llama a slice sin parámetros?

Cuando no se le pasa ningún argumento, slice devuelve una **copia completa** del _array_ original .

`console.log(animals.slice());` // ['ant', 'bison', 'camel', 'duck', 'elephant']

## ¿Por qué slice no modifica el array original?

Una característica fundamental de slice es su **inmutabilidad**: nunca altera el _array_ sobre el que se aplica. Siempre genera un _array_ nuevo con la porción solicitada . Esto permite ejecutar múltiples llamadas a slice sobre el mismo _array_ sin preocuparse por efectos secundarios.

En resumen, las formas de usar slice son:

- **Sin parámetros:** devuelve todo el _array_.
- **Un parámetro (inicio):** desde esa posición hasta el final.
- **Dos parámetros (inicio, fin):** desde inicio hasta fin sin incluir el fin.
- **Valores negativos:** cuentan desde el final del _array_.