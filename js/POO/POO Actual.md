Desde 2015, JavaScript incorporó una forma más clara y familiar de construir objetos: las **clases**. Aunque por debajo funcionan igual que las funciones constructoras tradicionales, su sintaxis se inspira en lenguajes como Java, lo que facilita la lectura y organización del código orientado a objetos. Entender cómo funcionan es fundamental para cualquier persona que quiera trabajar con programación moderna en JavaScript.

## ¿Qué es una clase y por qué se considera un _sugar syntax_?

Una clase en JavaScript es un **molde o _blueprint_** a partir del cual se construyen diferentes objetos . No introduce un mecanismo completamente nuevo; en realidad es una capa de sintaxis más limpia sobre el patrón de función constructora que ya existía. A esto se le conoce como _**sugar syntax**_: la misma funcionalidad con una escritura más legible.

Para declarar una clase se utiliza la palabra reservada `class`, seguida del nombre con la **primera letra en mayúscula**, por convención .

javascript class Persona { // contenido de la clase }

## ¿Cómo funciona el método constructor dentro de una clase?

El **constructor** es un método especial que define cómo se configuran las propiedades de cada objeto creado a partir de la clase . Recibe argumentos que permiten personalizar cada instancia.

javascript class Persona { constructor(nombre, edad) { this.nombre = nombre; this.edad = edad; } }

La palabra reservada **`this`** hace referencia a la propia instancia de la clase . Cuando escribimos `this.nombre = nombre`, estamos asignando el valor del parámetro recibido a la propiedad `nombre` del objeto que se está creando.

## ¿Qué son los métodos dentro de una clase?

Además de propiedades, una clase puede contener **métodos**: funciones que describen comportamientos del objeto . Se definen directamente dentro del cuerpo de la clase, sin necesidad de la palabra `function`.

class Persona { constructor(nombre, edad) { this.nombre = nombre; this.edad = edad; }

saludar() { console.log(`Hola, mi nombre es ${this.nombre} y tengo ${this.edad} años`); } }

El método `saludar` accede a las propiedades de la instancia mediante `this.nombre` y `this.edad`, e imprime un mensaje personalizado en consola .

## ¿Cómo se crea una nueva instancia con _new_?

Una clase por sí sola es solo un molde; no contiene valores concretos . Para generar un objeto real se utiliza la palabra reservada **`new`**, que conecta con el constructor y rellena las propiedades con los valores proporcionados .

javascript const persona1 = new Persona('Mariana', 25); persona1.saludar(); // Hola, mi nombre es Mariana y tengo 25 años

- **`new Persona('Mariana', 25)`** crea una nueva instancia de la clase `Persona`.
- Los valores `'Mariana'` y `25` se asignan a `this.nombre` y `this.edad` respectivamente.
- Al llamar `persona1.saludar()`, el método imprime el mensaje con los datos de esa instancia específica .

Este proceso se puede repetir tantas veces como se necesite para crear múltiples personas, cada una con sus propios valores, pero compartiendo la misma estructura y los mismos métodos definidos en la clase.

## ¿Por qué es importante dominar esta sintaxis?

A partir de esta versión del lenguaje, prácticamente todo el desarrollo orientado a objetos en JavaScript se construye con clases . Los elementos clave que debes recordar son:

- La palabra reservada **`class`** para declarar el molde.
- El método **`constructor`** para inicializar propiedades.
- La referencia **`this`** para acceder a las propiedades y métodos de la instancia.
- La palabra **`new`** para crear instancias concretas.
- Los **métodos** definidos dentro del cuerpo de la clase para agregar comportamiento.

Si ya trabajaste con funciones constructoras, notarás que la lógica es idéntica; lo que cambia es la forma de escribirlo, volviéndolo más organizado y cercano a otros lenguajes. ¿Ya probaste crear tus propias clases? Comparte en los comentarios qué estructura te resulta más cómoda.

![[Pasted image 20260611144714.png]]