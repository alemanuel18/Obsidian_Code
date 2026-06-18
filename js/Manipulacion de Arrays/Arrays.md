## ¿Qué es un array en programación?

Los arrays son fundamentales en la programación, permitiendo a los desarrolladores almacenar múltiples valores dentro de una sola variable. A menudo, las variables adquieren un único valor, pero los arrays ofrecen la capacidad de mantener un conjunto de elementos, lo que los hace increíblemente útiles en diversas situaciones. Además, es esencial saber que los arrays son objetos en JavaScript.

## ¿Cómo se crea un array?

Existen varias formas de crear un array en JavaScript. Vamos a explorar dos métodos populares:

1. **Usando `new Array()`**: Este enfoque requiere el uso de la palabra clave `new` seguida de `Array()`. Aunque es menos común, verás este método en proyectos más antiguos.
    
    ![[Pasted image 20260610191528.png]]
    
2. **Sintaxis literal del array**: Este es el método más utilizado. Consiste en usar corchetes `[]` para definir los elementos del array.
    
    ![[Pasted image 20260610191538.png]]
    

¿Cómo se manejan arrays con diferentes tipos de datos?

Una de las características sobresalientes de los arrays es su capacidad para almacenar diversos tipos de datos. Puedes combinarlos para tener strings, números, booleanos, e incluso otros objetos dentro del mismo array.

![[Pasted image 20260610191557.png]]

¿Cómo acceder a los elementos de un array?

Acceder a los elementos de un array se realiza mediante sus índices, comenzando desde cero. Por ejemplo, en el array `fruits`, `fruits[0]` devolvería `'apple'`.

![[Pasted image 20260610191610.png]]

¿Cómo se analiza el tamaño de un array?

Para conocer cuántos elementos contiene un array, se utiliza la propiedad `.length`. Esta devuelve un número representando la cantidad total de elementos.

![[Pasted image 20260610191618.png]]

Los arrays son herramientas poderosas en el mundo de la programación, facilitando la organización y manipulación de datos de manera eficiente. Continuar explorando sus capacidades y combinaciones enriquecerá tus habilidades como desarrollador. ¡Sigue practicando y te convertirás en un maestro de los arrays!

---

# Mutabilidad e inmutabilidad
Comprender cómo se comportan los arrays cuando los modificamos es fundamental para escribir código predecible en JavaScript. La diferencia entre **mutar** el array original o **crear uno nuevo** determina la forma en que gestionamos los datos y evitamos errores inesperados. A continuación se exploran estos conceptos junto con un ejercicio práctico que combina arrays y ciclos `for`.

## ¿Qué significa mutabilidad e inmutabilidad en arrays?

Un array en JavaScript es un objeto que dispone de múltiples métodos. Algunos de esos métodos **transforman el array original** (mutabilidad) y otros **generan un array completamente nuevo** sin alterar el anterior (inmutabilidad). Reconocer esta distinción es clave para decidir qué método usar en cada situación.

## ¿Cómo funciona un método mutable como push?

El método `.push()` agrega un elemento al final del array existente, modificándolo directamente .

js const fruits = ["apple", "banana", "orange"]; fruits.push("watermelon"); console.log(fruits); // ["apple", "banana", "orange", "watermelon"]

Al ejecutar este código, el array `fruits` ya no tiene tres elementos sino cuatro. **El array original fue mutado**, es decir, su contenido cambió permanentemente.

## ¿Cómo se logra la inmutabilidad con concat?

El método `.concat()` une dos arrays y devuelve uno nuevo, sin modificar ninguno de los originales .

js const newFruits = fruits.concat(["grape", "kiwi"]); console.log(fruits); // ["apple", "banana", "orange", "watermelon"] console.log(newFruits); // ["apple", "banana", "orange", "watermelon", "grape", "kiwi"]

Aquí `fruits` conserva sus cuatro elementos, mientras que `newFruits` contiene seis. **No se mutó el array original**; se creó una referencia distinta con los datos combinados.

## ¿Cómo verificar si una variable es un array?

JavaScript ofrece el método estático `Array.isArray()`, que recibe cualquier valor y devuelve un **booleano** (`true` o `false`) indicando si se trata de un array .

js const isArray = Array.isArray(fruits); console.log(isArray); // true

Esta comprobación resulta útil cuando recibimos datos de fuentes externas y necesitamos asegurarnos de que podemos iterar sobre ellos antes de aplicar métodos propios de arrays.

## ¿Cómo sumar todos los elementos de un array con un ciclo for?

Un ejercicio clásico para practicar arrays y ciclos consiste en **sumar todos los valores numéricos** contenidos en un array .

js const numbersArray = [1, 2, 3, 4, 5]; let sum = 0;

for (let i = 0; i < numbersArray.length; i++) { sum = sum + numbersArray[i]; }

console.log(sum); // 15

## ¿Qué papel juegan length y el índice en la iteración?

- **`numbersArray.length`** devuelve `5`, que es la cantidad total de elementos.
- La condición `i < numbersArray.length` garantiza que el índice llegue como máximo hasta `4`, evitando acceder a una posición inexistente.
- En cada vuelta del ciclo, `numbersArray[i]` obtiene el valor en la posición actual y lo **acumula** en la variable `sum`.

El resultado es `15` porque `1 + 2 + 3 + 4 + 5 = 15`. Este patrón de **acumulador** es muy común y sirve de base para operaciones más complejas como promedios o búsquedas de valores máximos.

Dominar la diferencia entre métodos mutables e inmutables, saber verificar tipos de datos y combinar arrays con estructuras de control como `for` son habilidades esenciales para cualquier persona que esté aprendiendo JavaScript. ¿Has probado a reemplazar `.push()` por el _spread operator_ para mantener la inmutabilidad? Comparte tu experiencia en los comentarios.

---

# Push y Pop
Cuando trabajas con arrays en JavaScript, es fundamental entender qué métodos **modifican el array original** y cuáles crean uno nuevo. Dos de los métodos más utilizados para alterar directamente un array son **push** y **pop**, y dominarlos es clave para manipular datos de forma eficiente.

## ¿Qué es la mutabilidad en arrays de JavaScript?

La **mutabilidad** (_mutability_) se refiere a la capacidad de cambiar un valor después de haberlo creado. Cuando usamos métodos como `push` o `pop`, no estamos generando un nuevo array, sino que estamos **modificando directamente el array original**. Esto es algo muy importante a tener en cuenta, porque cualquier referencia a ese array también verá los cambios reflejados.

## ¿Cómo funciona el método push para agregar elementos?

El método `push` **añade uno o más elementos al final de un array** y devuelve la nueva longitud de ese array . Veamos un ejemplo práctico:

javascript const countries = ['USA', 'Canada', 'UK']; const newCountries = countries.push('Germany', 'Australia');

console.log(countries); // ['USA', 'Canada', 'UK', 'Germany', 'Australia'] console.log(newCountries); // 5

- `push` recibe uno o varios valores como argumento.
- Los agrega al **final** del array original.
- Retorna un número: la **nueva longitud** del array.

En el ejemplo, el array `countries` pasa de tener tres elementos a cinco. La variable `newCountries` no contiene un array, sino el valor `5`, que representa esa nueva longitud . Es un detalle que muchos principiantes pasan por alto.

## ¿Por qué push modifica el array original?

Porque `push` es un método **mutante**. No crea una copia del array, sino que opera directamente sobre él. Si necesitas conservar el array sin cambios, deberías hacer una copia antes de usar `push`.

## ¿Cómo funciona el método pop para eliminar elementos?

El método `pop` hace lo contrario de `push`: **elimina el último elemento del array** y lo devuelve como valor . Observa el siguiente código:

javascript const countries = ['USA', 'Canada', 'UK', 'Germany', 'Australia']; const removedCountry = countries.pop();

console.log(countries); // ['USA', 'Canada', 'UK', 'Germany'] console.log(removedCountry); // 'Australia'

- `pop` no recibe argumentos.
- Remueve el **último elemento** del array.
- Retorna el **elemento eliminado**, no la longitud.

## ¿Qué diferencia hay entre lo que devuelven push y pop?

Esta es una distinción clave:

- **push** retorna la nueva **longitud** del array.
- **pop** retorna el **elemento que fue removido**.

Ambos métodos comparten una característica esencial: los dos **mutan el array original** . Después de aplicar `pop`, el array `countries` queda con un elemento menos, y esa modificación es permanente en la referencia original.

## ¿Cuándo usar push y pop en tus proyectos?

Estos métodos son ideales para estructuras de datos tipo **pila** (_stack_), donde el último elemento en entrar es el primero en salir (_LIFO_). Algunos casos de uso comunes:

- Agregar elementos a una lista dinámica con `push`.
- Deshacer la última acción eliminando el último elemento con `pop`.
- Controlar flujos donde necesitas ir apilando y desapilando valores.

Recuerda siempre que al ser métodos que generan mutabilidad, debes tener cuidado cuando compartas referencias al mismo array en distintas partes de tu código. Si otro fragmento depende del estado original, podrías encontrarte con comportamientos inesperados.