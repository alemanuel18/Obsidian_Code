## ¿Qué son las funciones puras?

En el vasto mundo de la programación, donde se busca la eficiencia y claridad del código, las funciones puras juegan un papel crucial. Se caracterizan por dos propiedades fundamentales que garantizan su comportamiento predecible y confiable:

- **Determinismo:** Dada una entrada particular, una función pura siempre produce la misma salida. Esto significa que no importa cuántas veces llames a la función con los mismos argumentos; el resultado será siempre el mismo.
- **Ausencia de efectos secundarios:** Estas funciones no alteran estados fuera de su propio entorno. Esto significa que no modifican variables globales ni interaccionan con elementos externos al código, como bases de datos o APIs.

A medida que exploramos estas funciones, descubrimos que son una pieza esencial en el diseño de software funcional, promoviendo un código más limpio y fácil de probar.

## ¿Cuáles son los efectos secundarios?

En contraste con las funciones puras, muchos programas dependen de efectos secundarios para cumplir con sus propósitos. Estos efectos secundarios, aunque esenciales en ciertos contextos, pueden hacer que el código sea impredecible. Algunos ejemplos incluyen:

- **Modificar variables globales:** Acceder y alterar variables fuera del alcance local de una función puede resultar en funciones impuras.
- **Modificar parámetros:** Cambiar los valores de los argumentos pasados a una función también genera efectos no deseados.
- **Solicitudes HTTP:** Llamadas a servicios externos o APIs pueden producir cambios basados en respuestas externas.
- **Impresión de mensajes:** Tanto `console.log` como `alert` son ejemplos de funciones que producen salidas visibles o auditables.
- **Manipulación del DOM:** Interacciones con la estructura del documento en navegadores, alterando su contenido o apariencia.
- **Consultas de tiempo:** Obtener la hora o fecha actual afecta al estado del programa de forma impredecible.

Aunque estos efectos pueden parecer negativos, es importante recordar que muchos son necesarios para las aplicaciones prácticas.

## ¿Cómo estructuramos una función pura?

Para entender mejor el concepto de función pura, es útil observar un ejemplo práctico. Imagina una función simple que sume dos números:

`function sum(a, b) {   return a + b; }`

Esta función es pura porque:

- Siempre devuelve el mismo resultado cuando se le proporcionan los mismos argumentos.
- No produce efectos secundarios ya que no altera ningún estado global ni interactúa con el entorno externo.

Sin embargo, ¿qué ocurre cuando introducimos una línea de código que imprime un valor en la consola?

`function sumYLog(a, b) {   console.log(a);   return a + b; }`

Al agregar `console.log`, la función deja de ser pura, ya que ahora produce un efecto secundario.

## Por qué son importantes las funciones puras?

Las funciones puras son esenciales en programación porque permiten:

1. **Facilidad de prueba:** Como no dependen del estado del programa ni lo modifican, son más fáciles de aislar y probar.
2. **Previsibilidad y confiabilidad:** Siempre ofrecen el mismo resultado para los mismos inputs, facilitando la comprensión del flujo del programa.
3. **Optimización y paralelismo:** Facilitan optimizaciones como la memoización (almacenamiento de resultados previos) y son ideales para programas concurrentes o paralelizados.

_Funciones como `square` o `attain`, que realizan operaciones matemáticas básicas con un único parámetro, son ejemplos clásicos de funciones puras con resultados predecibles._

## ¿Qué ocurre con la combinación de funciones puras?

La combinación de funciones puras también resulta en funciones puras. Por ejemplo, combinando las funciones `square` y `attain`, podemos crear un árbol robusto de funciones:

`function square(x) {   return x * x; } function attain(y) {   return y + 10; } const number = 5; const finalResult = attain(square(number)); // finalResult será 35`

Esta combinación sigue manteniendo la pureza y ofrece la garantía de resultados constantes sin efectos adicionales.

En resumen, el balance entre funciones puras e impuras es vital para escribir un código robusto y escalable. Al comprender y aplicar estos conceptos, los programadores pueden crear software más predecible, fácil de mantener y testar. ¡Sigue explorando y refinando tus habilidades en programación!