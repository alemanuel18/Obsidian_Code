Controlar la repetición de instrucciones es fundamental en cualquier lenguaje de programación. El ciclo **while** permite ejecutar un bloque de código una y otra vez **mientras una condición sea verdadera**, y entender su estructura evita errores críticos como los temidos loops infinitos.

## ¿Cómo funciona la estructura del ciclo while?

El **while** es una palabra reservada de JavaScript que recibe una condición entre paréntesis. Mientras esa condición se evalúe como `true`, el código que está dentro de las llaves se ejecutará de forma repetida . En el momento en que la condición deje de cumplirse, el ciclo se rompe y el programa continúa con el resto del código.

La estructura básica luce así:

`while (condición) { // código que se repite }`

- La **condición** se evalúa antes de cada iteración.
- Si desde el inicio la condición es `false`, el bloque nunca se ejecuta.
- Todo lo que esté dentro de las llaves se repite en cada vuelta del ciclo.

## ¿Qué es un loop infinito y por qué hay que evitarlo?

Si la condición dentro de **while** nunca deja de ser verdadera, el ciclo se repite de manera indefinida . Esto se conoce como **loop infinito** y puede consumir toda la memoria RAM del navegador, provocando que la pestaña o incluso el navegador completo deje de responder y termine por _crashear_. Por eso, es indispensable asegurarse de que algo dentro del bloque modifique la condición para que en algún momento se evalúe como `false`.

## ¿Cómo se usa while con un contador práctico?

Un patrón muy común es declarar una variable que funcione como **contador** y que se incremente en cada iteración hasta alcanzar un límite definido en la condición .

```
let contador = 0;

while (contador < 10) { console.log(contador); contador++; }
```
El flujo paso a paso es el siguiente:

- Se crea la variable `contador` con valor inicial **0**.
- **while** verifica si `contador` es menor a 10; como 0 es menor a 10, entra al bloque.
- `console.log(contador)` imprime el valor actual en la consola.
- `contador++` incrementa el valor en 1, de modo que en la siguiente vuelta ya no es 0 sino 1.
- El ciclo se repite: 1 sigue siendo menor a 10, luego 2, luego 3… hasta llegar a 9.
- Cuando `contador` vale **10**, la condición `10 < 10` es `false` y el ciclo se detiene.

El resultado en consola son los números del **0 al 9**, es decir, 10 impresiones en total .

## ¿Qué pasa si olvidamos incrementar el contador?

Sin la línea `contador++`, la variable siempre conserva el valor 0 y la condición `0 < 10` jamás deja de cumplirse . Esto genera exactamente el **loop infinito** mencionado antes: el navegador se queda ejecutando `console.log(0)` sin parar hasta agotar los recursos del sistema.

## ¿Cuáles son las mejores prácticas al usar while?

Para aprovechar el ciclo **while** de forma segura, ten en cuenta lo siguiente:

- **Define siempre una variable de control** antes del ciclo, como el contador.
- **Modifica esa variable dentro del bloque** para que la condición eventualmente sea `false`.
- **Verifica la lógica de la condición** antes de ejecutar; pregúntate en qué momento dejará de ser verdadera.
- Usa `while` cuando **no conozcas de antemano** cuántas veces necesitas iterar; si lo sabes, un `for` puede ser más adecuado.

El operador `++` que se usa en `contador++` es el operador de **incremento**, y suma exactamente 1 al valor actual de la variable en cada iteración. Sin él, el patrón de contador simplemente no funciona.

Si ya probaste el ejemplo y viste los números del 0 al 9 en tu consola, intenta cambiar la condición o el valor inicial del contador y observa cómo se comporta el ciclo. Comparte en los comentarios qué variaciones lograste.