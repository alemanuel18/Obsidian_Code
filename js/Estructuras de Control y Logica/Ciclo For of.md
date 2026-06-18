Cuando necesitas recorrer los elementos de un _array_ o un _string_ de forma clara y directa, **for of** se convierte en tu mejor aliado. Este método de iteración en JavaScript simplifica la lectura del código y reduce errores comunes al trabajar con listas, ya que se enfoca exclusivamente en los **valores** de cada elemento.

## ¿Qué es for of y cuándo se utiliza?

El nombre lo dice todo: **for** (por cada) **of** (de). Es decir, por cada elemento de cierta colección, ejecuta un bloque de código. La clave está en entender que **for of solo funciona con objetos iterables** . ¿Y qué son objetos iterables? Son estructuras que internamente representan una lista ordenada de valores. Los dos ejemplos principales son:

- _Arrays_: listas de elementos como números, textos u otros objetos.
- _Strings_: cadenas de texto, que internamente son listas de caracteres.

Cualquier objeto al que puedas aplicar la propiedad `.length` y obtener una longitud es, en esencia, una lista que puedes recorrer con **for of** .

## ¿Cuál es la estructura base de for of?

La sintaxis es limpia y fácil de recordar :

`for (let variable of objeto) { // código a ejecutar }`

El ciclo toma cada valor del objeto iterable, lo asigna a la variable declarada y ejecuta el bloque de código. Cuando **ya no quedan elementos en la lista**, el _loop_ se detiene automáticamente, como si se generara un _break_ implícito . No necesitas controlar índices ni condiciones adicionales.

## ¿Cómo se aplica for of con un array de frutas?

Un ejemplo práctico ayuda a consolidar la idea. Imagina una canasta de frutas :

```
let canasta = ["manzana", "pera", "naranja", "uva"];

for (let fruta of canasta) { console.log(fruta); }
```

El resultado en la consola del navegador será:

- manzana.
- pera.
- naranja.
- uva.

La lectura es prácticamente natural: **por cada fruta de la canasta, imprímela** . Cuando la lista se agota, la iteración se rompe y el programa continúa con el código siguiente.

## ¿Por qué nombrar la variable según el contexto?

Una buena práctica al usar **for of** es darle a la variable un nombre que represente el elemento individual de la colección . Si tienes una lista llamada `canasta` que contiene frutas, la variable se llama `fruta`. Si tuvieras una lista de `usuarios`, la variable sería `usuario`. Esto hace que el código sea **autodocumentado** y mucho más legible para cualquier persona que lo revise.

## ¿Cómo saber si un objeto es iterable?

Una forma rápida de verificar si puedes aplicar **for of** sobre un objeto es comprobar su propiedad `.length` . Si al escribir `canasta.length` obtienes un número, estás frente a un objeto iterable que puedes recorrer sin problema.

Recuerda que **for of** no está diseñado para objetos literales comunes (los que se crean con llaves `{}`). Para esos casos existen otros métodos de iteración. Aquí lo importante es distinguir: si es una **lista con longitud**, usa **for of**.

Si ya dominas el _for_ tradicional, incorporar **for of** a tu práctica diaria te permitirá escribir código más conciso y expresivo. ¿Con qué tipo de listas lo probarías primero?