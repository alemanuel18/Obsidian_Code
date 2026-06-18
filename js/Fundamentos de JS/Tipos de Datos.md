Conocer los **diez tipos de datos de JavaScript** es el primer paso para escribir código con confianza. Se agrupan en dos grandes familias —**primitivos** y **complejos**— y cada uno cumple un rol específico a la hora de representar información. A continuación se explica cómo se declaran y cuándo conviene usar cada uno.

## ¿Cuáles son los siete tipos de datos primitivos en JavaScript?

Los datos primitivos son valores simples e inmutables. JavaScript ofrece siete y cada uno resuelve una necesidad distinta.

## ¿Cómo funcionan _string_, _number_ y _boolean_?

- _**String**_ : representa una cadena de caracteres. Se escribe entre comillas simples o dobles. Por ejemplo: `let nombre = 'Tere';`. El punto y coma al final es opcional porque JavaScript lo añade automáticamente.
- _**Number**_ : almacena valores numéricos. Se declara directamente con el número: `let edad = 25;`.
- _**Boolean**_ : solo admite dos valores, `true` o `false`. Es útil para expresar condiciones como `let esMayorDeEdad = true;`.

```
let nombre = "Alemanuel"
let edad = "20"
let mayorEdad = true
```

## ¿Qué diferencia hay entre _null_ y _undefined_?

- _**Null**_ : indica un **vacío intencional**. Lo asignamos nosotros como programadores para señalar que una variable no contiene valor: `let noHayValor = null;`.
- _**Undefined**_ : aparece cuando JavaScript detecta que **no se ha definido** ningún valor. Normalmente no lo asignamos manualmente; es el propio lenguaje el que lo devuelve cuando algo no existe o no se ha inicializado: `let noDefinido = undefined;`.

```
let valor = null

let definido 0 undefined
```

La distinción clave es que **null es una decisión del programador**, mientras que **undefined es una respuesta del lenguaje**.

## ¿Para qué sirven _symbol_ y _BigInt_?

- _**Symbol**_ : genera un **valor único e irrepetible**, ideal para identificadores como IDs de usuario. Se escribe así: `let simboloUnico = Symbol('unico');`. La función `Symbol()` garantiza que no habrá otro valor igual.
- _**BigInt**_ : permite trabajar con **números extremadamente grandes** que superan el límite de _Number_. Se declara añadiendo una `n` al final del número: `let numeroGrande = 2n;`. Es útil cuando se necesitan cálculos con cifras de gran magnitud.

```
let simboloUnico = Symbol ('unico')

let numeroGrante = 2n
```

## ¿Cómo se escriben los tipos de datos complejos?

Los tipos complejos pueden contener múltiples valores y estructuras más elaboradas. JavaScript cuenta con tres: **objetos**, **arrays** y **funciones**.

## ¿Qué es un objeto y cómo se declara?

Un **objeto** (_object_) agrupa varias características bajo un mismo nombre. Se escribe con llaves y pares de propiedad-valor separados por comas:

javascript let carro = { marca: 'Tesla', modelo: 'Model S' };

Cada propiedad —como `marca` o `modelo`— describe un aspecto del elemento que representamos. Es la estructura perfecta cuando algo tiene **múltiples atributos relacionados**.

```
let carro ={
	marca: 'Kia'
	modelo: 2007
}

```

## ¿Cuándo usar un _array_ y cuándo una función?

- _**Array**_ : almacena un **conjunto ordenado de elementos**. En otros lenguajes se conocen como listas. Se escribe con corchetes:
```
let frutas = [
'manzana', 'banano', 'uvas'
];

```

Siempre que necesites agrupar varios valores del mismo tipo, un _array_ es la opción indicada.

- _**Función**_  (_function_) : es un bloque de código reutilizable. Se declara con la palabra clave `function`, un nombre, parámetros entre paréntesis y un cuerpo entre llaves:

```
function saludar(nombre) { 
	let saludo = 'Hola, como te encuentras hoy, ${nombre}.'
	return saludo
}
```
Los **paréntesis** reciben la información que la función necesita para trabajar, y las **llaves** contienen las instrucciones que se ejecutarán. Existen otras formas de escribirlas, pero esta sintaxis es la base para comprender cómo operan.

Dominar estos diez tipos de datos te dará claridad para decidir qué estructura usar en cada situación. Si tienes dudas sobre alguno, comparte tu pregunta en los comentarios.