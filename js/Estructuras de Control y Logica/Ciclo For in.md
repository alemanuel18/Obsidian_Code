Cuando trabajas con estructuras de datos en JavaScript, no todo se resuelve con _arrays_ o _strings_. Los **objetos** representan información de manera distinta: cada dato tiene un nombre (propiedad) y un valor asociado. Para recorrer esas propiedades existe una herramienta específica llamada **for-in**, y entender cuándo y cómo usarla marca la diferencia entre código funcional y errores inesperados.

## ¿Qué es un objeto y en qué se diferencia de un array?

Un **objeto** es una estructura de datos que almacena información en pares de **propiedad y valor** . A diferencia de un _array_, que simplemente genera una lista de elementos, un objeto necesita siempre esa relación entre la propiedad (el nombre) y su valor correspondiente.

Por ejemplo, una lista de compras como objeto se vería así:

`const listaDeCompras = { manzana: 5, pera: 3, naranja: 2, uva: 1 };`

Aquí `manzana`, `pera`, `naranja` y `uva` son las **propiedades**, mientras que `5`, `3`, `2` y `1` son sus **valores**. Este objeto contiene cuatro propiedades, cada una con un dato asociado.

## ¿Cómo funciona la estructura del for-in?

La sintaxis del **for-in** sigue un patrón claro :

`for (variable in objeto) { // código a ejecutar }

- **`for`:** palabra reservada que inicia el ciclo.
- **`variable`:** almacena la propiedad actual en cada iteración.
- **`in`:** indica sobre qué objeto se itera.
- **`objeto`:** la estructura enumerable que se recorre.

La traducción es directa: por cada propiedad en este objeto, ejecuta el bloque de código.

## ¿Cómo obtener solo las propiedades?

Si únicamente necesitas los nombres de las propiedades, basta con imprimir la variable del ciclo :

`for (let fruta in listaDeCompras) { 
`console.log(fruta); 
`} // manzana // pera // naranja // uva

## ¿Cómo acceder al valor de cada propiedad?

Para obtener tanto la propiedad como su valor, se utiliza la notación de **corchetes cuadrados** sobre el objeto :

`for (let fruta in listaDeCompras) { 
`console.log(fruta, listaDeCompras[fruta]); 
`} // manzana 5 // pera 3 // naranja 2 // uva 1

Lo que sucede internamente es que la variable `fruta` actúa como un **índice** que referencia cada propiedad del objeto. En cada iteración, ese índice cambia y apunta a la siguiente propiedad, permitiendo extraer su valor con `listaDeCompras[fruta]` .

## ¿Cuál es la diferencia entre for-in y for-of?

Esta distinción es fundamental y fuente común de errores. JavaScript clasifica las estructuras de datos en dos categorías para efectos de iteración:

- **Objetos iterables:** _arrays_ y _strings_. Se recorren con **for-of**.
- **Objetos enumerables:** objetos con propiedades. Se recorren con **for-in**.

Si intentas usar **for-of** con un objeto, JavaScript lanza un error claro :

`for (let fruta of listaDeCompras) { 
`console.log(fruta); 
`} // TypeError: listaDeCompras is not iterable

El mensaje `"is not iterable"` confirma que los objetos no son iterables, son **enumerables**. Por eso necesitan su propio método de recorrido.

La regla práctica es sencilla:

- **for-in** → para objetos con propiedades y valores.
- **for-of** → para _arrays_ y _strings_.

Confundir estos dos métodos es uno de los errores más frecuentes al empezar con JavaScript. Ahora que conoces la diferencia entre estructuras iterables y enumerables, ¿en qué otros escenarios crees que sería útil aplicar **for-in** en tus proyectos?