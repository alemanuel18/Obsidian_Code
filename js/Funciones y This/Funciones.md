Imagina que estás en pleno _Black Friday_, rodeado de ofertas, con decenas de prendas en la mano y sin saber cuánto pagarás realmente por cada una. Esa situación cotidiana es perfecta para entender por qué las **funciones en JavaScript** son una de las herramientas más poderosas que puedes aprender. Una función es un fragmento de código reutilizable, como una pieza de Lego que puedes ensamblar una y otra vez para construir lo que necesites.

## ¿Qué es una función y por qué se compara con piezas de Lego?

Las funciones son **bloques de código genéricos** que encapsulan una tarea específica para ejecutarla cuantas veces sea necesario sin reescribir la lógica . Así como con un set de Lego puedes armar edificios, carros o casas usando las mismas fichas, con una función defines la lógica una vez y la aplicas a distintos datos.

En el ejemplo del _Black Friday_, cada prenda tiene un precio original y un porcentaje de descuento, pero no tienes el precio final. Hacer ese cálculo manualmente con cada artículo consume tiempo. Una función resuelve eso: le entregas el precio y el porcentaje, y ella te devuelve el valor que debes pagar .

Antes de escribir código, conviene identificar dos elementos esenciales:

- **Inputs (entradas):** los datos que alimentan al programa, como el precio y el porcentaje de descuento.
- **Output (salida):** el resultado esperado, en este caso el precio final con descuento aplicado.

## ¿Cuál es la anatomía de una función en JavaScript?

Cada función tiene partes bien definidas que conviene reconocer :

- **Palabra clave `function`:** indica al intérprete que estás declarando una función.
- **Nombre:** se escribe en _camelCase_, donde la primera letra va en minúscula y cada palabra siguiente inicia con mayúscula.
- **Parámetros:** van entre paréntesis y representan las entradas. Son opcionales; no todas las funciones los requieren.
- **Llaves `{}`:** delimitan el cuerpo de la función, es decir, el bloque donde vive toda la lógica.
- **`return`:** devuelve un valor al exterior. También es opcional; una función puede ejecutar código sin retornar nada.
- **Llamado o invocación:** se ejecuta escribiendo el nombre de la función seguido de paréntesis con los **argumentos**, que son los valores reales que sustituyen a los parámetros .

## ¿Cuál es la diferencia entre parámetros y argumentos?

Los **parámetros** son las variables genéricas declaradas en la definición de la función. Los **argumentos** son los valores concretos que pasas al momento de invocarla. Por ejemplo, si la función `suma` recibe `a` y `b` como parámetros, al llamarla con `suma(3, 5)` los números 3 y 5 son los argumentos .

## ¿Cómo crear una función para calcular precios con descuento?

Con la teoría clara, el paso siguiente es escribir el código. La función `calculateDiscountedPrice` recibe dos parámetros: `price` y `discountPercentage` .

```
function calculateDiscountedPrice (price, discountPercentage) { 
	const discount = (price * discountPercentage) / 100; 
	const priceWithDiscount = price - discount; 
	return priceWithDiscount;
}
```
La fórmula es directa: se multiplica el precio por el porcentaje y se divide entre cien para obtener el monto del descuento. Luego se resta al precio original y se retorna el resultado.

## ¿Cómo se invoca y se verifica el resultado?

Para ejecutar la función basta con asignar valores a las variables de entrada y llamarla con esos argumentos :

```
const originalPrice = 100; 
const discountPercentage = 20; 
const finalPrice = calculateDiscountedPrice(originalPrice, discountPercentage);

console.log("Original price: " + originalPrice); 
console.log("Discount: " + discountPercentage); 
console.log("Price with discount: " + finalPrice);
```
Al correr el programa con `node`, la consola muestra:

- Precio original: **100**.
- Descuento: **20 %**.
- Precio final: **80**.

Si cambias `originalPrice` a otro valor y `discountPercentage` a 15, el programa recalcula automáticamente sin modificar la función . Esa es la esencia de la **reutilización**: un mismo bloque de código sirve para todas las prendas que quieras evaluar.

Ahora que sabes construir funciones reutilizables, prueba a extender este ejemplo: agrega un tercer parámetro para el impuesto o crea una función que compare dos precios con descuento y te diga cuál es la mejor oferta. Comparte tu solución en los comentarios.