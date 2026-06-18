Dominar la iteración sobre arrays es fundamental para cualquier persona que trabaje con JavaScript. Dos métodos destacan por su capacidad de recorrer elementos sin modificar el array original: **map** y **forEach**. Aunque ambos ejecutan una función sobre cada elemento, su comportamiento y lo que devuelven es completamente distinto, y entender esa diferencia marca un antes y un después en la forma de escribir código limpio.

## ¿Cómo funciona el método map en JavaScript?

El método **map** es uno de los más utilizados en arrays. Su propósito es **aplicar una función a cada elemento** y construir un **nuevo array** con los resultados . El array original permanece intacto, lo que lo convierte en una herramienta segura cuando no queremos mutar datos.

Por ejemplo, dado un array de números del uno al cinco, se puede elevar cada número al cuadrado:

![[Pasted image 20260611102726.png]]
![[Pasted image 20260611102746.png]]

- Cada elemento pasa por la _arrow function_ que lo multiplica por sí mismo.
- El resultado se almacena en un **nuevo array** sin alterar el original.
- La función recibe como parámetro cada valor de forma individual.

Este patrón es especialmente útil cuando necesitas **transformar datos** y conservar la referencia original.

## ¿Qué diferencia a forEach de map?

El método **forEach** también itera sobre cada elemento y ejecuta una función proporcionada, pero **no devuelve un nuevo array** . Su valor de retorno es `undefined`. Esto significa que sirve para ejecutar acciones secundarias, como imprimir valores, pero no para generar una nueva colección.

![[Pasted image 20260611102857.png]]
![[Pasted image 20260611102916.png]]

- El _console.log_ dentro del _callback_ imprime cada color: _red_, _pink_, _blue_.
- Sin embargo, la variable `iteratedColors` queda como **indefinido**.
- El array original tampoco sufre modificación alguna.

La clave está en que **forEach ejecuta efectos secundarios**, mientras que **map produce un resultado almacenable**.

## ¿Cuándo usar map y cuándo forEach en ejercicios prácticos?

### ¿Cómo convertir temperaturas de Fahrenheit a Celsius con map?

Cuando necesitas un array nuevo con valores transformados, **map es la elección correcta** . En este ejercicio se toman temperaturas en Fahrenheit y se aplica la fórmula `(5/9) * (fahrenheit - 32)` a cada elemento:

![[Pasted image 20260611103222.png]]
const temperaturasEnCelsius = temperaturasEnFahrenheit.map( fahrenheit => (5 / 9) * (fahrenheit - 32) );
![[Pasted image 20260611103237.png]]

- Se obtiene un **array nuevo** con las temperaturas convertidas.
- El array original no se muta en ningún momento.
- Cada posición del nuevo array corresponde al resultado de aplicar la fórmula sobre la posición equivalente del original.

## ¿Cómo sumar todos los elementos de un array con forEach?

Cuando el objetivo no es crear un array sino **acumular un valor**, forEach resulta más adecuado . Aquí se calcula la suma de todos los números:

![[Pasted image 20260611103550.png]]

![[Pasted image 20260611103540.png]]

- La variable `suma` se inicializa en cero y se incrementa con cada iteración.
- El operador `+=` es un atajo para `suma = suma + number`.
- No se necesita un array de salida, solo un **valor acumulado**.

La regla general es sencilla: si necesitas **un nuevo array transformado**, usa **map**. Si necesitas **ejecutar una acción por cada elemento** sin generar un array, usa **forEach**. Cuéntanos en los comentarios si lograste identificar cuál método correspondía a cada ejercicio antes de ver la solución.