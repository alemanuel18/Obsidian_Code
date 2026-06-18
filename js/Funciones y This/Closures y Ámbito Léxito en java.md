Comprender cómo una función puede **recordar variables de su entorno exterior**, incluso después de haberse ejecutado, es fundamental para escribir código flexible y potente en JavaScript. Esto es exactamente lo que logran los _closures_, y dominar este concepto marca una diferencia importante en la forma de estructurar aplicaciones.

## ¿Qué es un closure y cómo se relaciona con el ámbito léxico?

Un **closure** es una función que tiene acceso a variables de un ámbito externo, incluso después de que esa función externa ya haya terminado de ejecutarse . Para comprender esta idea es necesario conocer el **ámbito léxico** (_lexical scope_): cuando una función se declara, se crea un ámbito léxico que le permite acceder tanto a sus propias variables como a las de ámbitos superiores .

En la práctica esto significa que si dentro de una función externa (_outer function_) se define una función interna (_inner function_), esta última puede leer y utilizar las variables de la primera.

## ¿Cómo se ve un closure en código?

El ejemplo más directo consiste en crear una función `outerFunction` con una variable `outerVariable` que contiene el texto `"I am from Outer function"` . Dentro de ella se define `innerFunction`, que ejecuta un `console.log` de esa variable externa y luego se retorna .

![[Pasted image 20260610154612.png]]
Al ejecutar el programa, la consola muestra `I am from Outer function` . Esto confirma que `innerFunction` **accedió a la variable de su función contenedora**, y eso es precisamente un _closure_.

## ¿Por qué hay que tener cuidado con el uso de memoria?

Los _closures_ conservan referencias a las variables externas, lo que implica consumo de memoria. Para ilustrarlo se crea una función `createCounter` con una variable `count` inicializada en cero . Internamente retorna una función que incrementa `count` con `count++` y lo imprime con `console.log` 
![[Pasted image 20260610154814.png]]
![[Pasted image 20260610154727.png]]
Cada llamada a `createCounter` genera **un ámbito léxico independiente** . Por eso `counterA` llega a 2 mientras `counterB` arranca en 1: cada instancia almacena su propio valor de `count` en memoria.  Esto demuestra que, aunque los _closures_ son muy útiles, conviene **no abusar de ellos** para evitar un consumo excesivo de recursos .

## ¿Cómo manejar diferentes contextos con closures?

Otro uso práctico es generar funciones con **contextos distintos** a partir de una misma estructura. Se crea una función `other` con una variable `message` que contiene `"Hello, "` . Dentro se define `inner`, que recibe un parámetro `name` y lo concatena con el mensaje externo .

![[Pasted image 20260610155051.png]]
![[Pasted image 20260610155136.png]]

Al ejecutar se obtiene `Hello, Alice` y `Hello, Bob` . Cada _closure_ mantiene su propio contexto pero comparte la misma lógica interna, lo que permite crear **funciones flexibles y reutilizables**.

## ¿Qué ventajas ofrecen los closures en la práctica?

- Permiten trabajar con **diferentes ámbitos** dentro de una misma estructura de funciones.
- Facilitan la creación de funciones que **recuerdan estado** entre ejecuciones, como contadores o acumuladores.
- Hacen posible generar **múltiples contextos** a partir de una sola función base, personalizando el comportamiento con parámetros.
- Su uso debe ser **consciente y medido**, ya que cada _closure_ retiene referencias en memoria que no se liberan automáticamente .

Si ya has experimentado con _closures_ en tus proyectos o tienes dudas sobre cómo aplicarlos de forma eficiente, comparte tu experiencia en los comentarios.