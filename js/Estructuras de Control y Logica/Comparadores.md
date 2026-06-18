Comprender cómo comparar valores es el primer paso para escribir código que tome decisiones. En JavaScript, los **operadores de comparación** permiten evaluar relaciones entre datos y devolver `true` o `false`, resultado que después se aprovecha en las estructuras de **ejecución condicional**. A continuación se explican cada uno de estos operadores con ejemplos prácticos ejecutados directamente en la consola del navegador.

## ¿Qué son los operadores de comparación y por qué importan?

Los operadores de comparación son símbolos que confrontan dos valores y generan un resultado booleano: **verdadero** (`true`) o **falso** (`false`). Ese resultado es la base de toda condición en un programa; sin él, el código no podría decidir qué camino seguir.

## ¿Cuál es la diferencia entre igualdad simple y estricta?

- El operador **doble igual** (`==`) compara únicamente si dos valores son iguales, sin importar el tipo de dato .
- El operador **triple igual** (`===`) compara el valor **y** el tipo de dato al mismo tiempo . Si ambos coinciden, devuelve `true`; de lo contrario, devuelve `false`.

Se recomienda **siempre utilizar el triple igual** porque ayuda a evitar errores sutiles provocados por la coerción automática de tipos que hace JavaScript.

## ¿Cómo funcionan los operadores de desigualdad?

- El operador **diferente** (`!=`) verifica si un valor es distinto a otro. Si son distintos, retorna `true` .
- El operador **estrictamente diferente** (`!==`) verifica diferencia tanto en valor como en tipo de dato . Al igual que con la igualdad, conviene usar esta versión para prevenir comportamientos inesperados.

## ¿Qué hacen los operadores mayor, menor y sus variantes?

- **Mayor que** (`>`): devuelve `true` cuando el valor de la izquierda supera al de la derecha .
- **Menor que** (`<`): devuelve `true` cuando el valor de la izquierda es inferior al de la derecha .
- **Mayor o igual** (`>=`): devuelve `true` cuando el valor es mayor o exactamente igual .
- **Menor o igual** (`<=`): devuelve `true` cuando el valor es menor o exactamente igual .

## ¿Cómo probar estos operadores en la consola del navegador?

Para experimentar con estos operadores basta con abrir la **consola del navegador**, ya que el navegador interpreta JavaScript de forma nativa. El ejemplo parte de tres constantes :

javascript const a = 10; const b = 20; const c = "10";

La variable `a` almacena el número `10`, `b` almacena `20` y `c` almacena la cadena de texto `"10"`. Esta diferencia de tipo de dato entre `a` y `c` es clave para entender la igualdad estricta.

## ¿Qué resultados arrojan las comparaciones?

- `a == b` → `false`, porque `10` no es igual a `20` .
- `a === c` → `false`, porque aunque ambos representan "diez", `a` es de tipo _number_ y `c` es de tipo _string_ .
- `a != b` → `true`, porque `10` es diferente de `20` .
- `a !== c` → `true`, porque difieren en el tipo de dato .
- `a > b` → `false`, porque `10` no es mayor que `20` .
- `a <= b` → `true`, porque `10` es menor que `20` .
- `a > c` → `false`, porque `10` no es mayor que `10` .

## ¿Por qué preferir la comparación estricta?

JavaScript realiza **coerción de tipos** cuando se usa `==` o `!=`. Esto significa que convierte internamente un tipo de dato a otro para intentar que la comparación funcione, lo cual puede producir resultados inesperados. Con `===` y `!==` esa conversión no ocurre: si el tipo no coincide, el resultado es `false` de inmediato. Adoptar esta práctica desde el inicio genera código más predecible y reduce significativamente los _bugs_.

Dominar estos operadores es el requisito previo para trabajar con estructuras como `if`, `else` y `switch`, donde cada decisión depende del booleano que estas comparaciones devuelven. ¿Ya probaste combinar varios operadores en la consola? Comparte tus resultados y dudas en los comentarios.