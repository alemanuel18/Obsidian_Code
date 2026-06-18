Cuando trabajas con ciclos en JavaScript, es fundamental conocer todas las herramientas disponibles para repetir bloques de código de manera controlada. El **do while** es una estructura que garantiza la ejecución del código al menos una vez antes de evaluar cualquier condición, y entender su diferencia con el _while_ tradicional marca la diferencia al momento de elegir la solución correcta para cada problema.

## ¿Cómo se estructura un do while en JavaScript?

La construcción de un **do while** sigue un orden particular que lo distingue de otros ciclos. Primero se escribe la palabra reservada `do`, seguida de llaves (_brackets_) donde se coloca el código que se desea ejecutar. Después, se agrega el `while` con la condición que debe cumplirse para que el ciclo continúe repitiéndose .

```
do { // código que se ejecuta } 
while (condición);
```

Esta estructura significa que:

- El bloque de código dentro del `do` **se ejecuta primero**.
- Luego se evalúa la condición en el `while`.
- Si la condición sigue siendo verdadera, el ciclo regresa al `do`.
- Cuando la condición deja de cumplirse, se produce un _break_ automático y el ciclo se rompe.

## ¿Cómo se ve un ejemplo práctico de do while?

Para entender mejor su funcionamiento, se puede construir un contador sencillo :

```
let contador = 0;

do { console.log(contador); contador++; } 
while (contador < 10);
```
En este ejemplo, la variable `contador` inicia en cero. Dentro del `do`, se imprime el valor actual con `console.log` y luego se **incrementa en uno** para evitar caer en un _loop_ infinito. La condición del `while` establece que el ciclo continúe mientras `contador` sea menor a 10. El resultado es la impresión de los números del 0 al 9 .

## ¿Cuál es la diferencia entre while y do while?

La **diferencia principal** radica en el momento en que se evalúa la condición :

- En un **do while**, el código se ejecuta **antes** de validar la condición. Esto garantiza que el bloque de código se ejecute al menos una vez, sin importar si la condición es verdadera o falsa desde el inicio.
- En un **while**, la condición se valida **antes** de ejecutar el código. Si la condición es falsa desde el principio, el código nunca se ejecuta.

## ¿Cuándo conviene usar do while en lugar de while?

El caso de uso es claro: si necesitas que el código **se ejecute al menos una vez** antes de comprobar si debe repetirse, el **do while** es la opción correcta. Por ejemplo, cuando solicitas datos al usuario y necesitas mostrar algo antes de verificar si la entrada es válida .

Por otro lado, si lo que necesitas es **validar primero** que una condición sea verdadera antes de ejecutar cualquier lógica, entonces un `while` convencional es más adecuado.

Comprender cuándo aplicar cada tipo de ciclo te permite escribir código más preciso y evitar errores lógicos. Si has trabajado con ambos ciclos, comparte en los comentarios en qué situaciones has preferido usar **do while** sobre **while**.