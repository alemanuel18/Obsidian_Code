## ¿Cuál es el tipo de dato `number` en JavaScript?

En JavaScript, el tipo de dato primitivo `number` es esencial para el manejo de operaciones numéricas. Aunque existen diversas formas de escribir números, como enteros y decimales, todos se reconocen bajo el mismo tipo de dato: `number`. Esta unificación facilita la manipulación y el cálculo numérico. Veamos cómo se representan en este lenguaje:

- **Enteros y decimales**: Se escriben de forma diferente, pero en su naturaleza subyacente ambos son números.
    
    `let entero = 42; let decimal = 3.14; console.log(typeof entero); // "number" console.log(typeof decimal); // "number"`
    
- **Notación científica**: En JavaScript, también podemos utilizar la notación científica para representar números. Se usa la letra `e` para indicar una potencia de 10.
    
    `let cientifico = 5e3; // equivale a 5000`
    
- **Infinity y NaN**: La representación de números infinitos usa `Infinity`, mientras que un cálculo o valor indefinido se representa como `NaN` (Not a Number).
    
    `let infinito = Infinity; let noNumero = NaN;`
    

## ¿Cómo realizar operaciones aritméticas?

JavaScript proporciona operadores aritméticos para realizar cálculos básicos y avanzados. Entre ellos destacan:

Operaciones básicas

- **Suma (+)**: Adición de dos números.
- **Resta (-)**: Diferencia entre dos números.
- **Multiplicación (*)**: Producto de dos números.
- **División (/)**: Cociente de dos números.

`let suma = 5 + 3; let resta = 10 - 6; let multiplicacion = 2 * 3; let division = 9 / 3;`

Operaciones avanzadas

- **Módulo (%)**: Retorna el residuo de una división entre dos números. Útil para saber si un número es múltiplo de otro.
    
    `let modulo = 10 % 3; // resultado es 1`
    
- **Exponenciación (**)**: Eleva un número a una potencia específica.
    
    `let potencia = 2 ** 3; // equivale a 8`
    

Dilemas con la precisión

JavaScript a veces enfrenta problemas de precisión en operaciones decimales.

- **Ejemplo**: Al sumar 0.1 y 0.2, podríamos esperar 0.3, pero el resultado podría ser un número decimal largo y preciso.
    
    `let resultado = 0.1 + 0.2; console.log(resultado); // Imprime algo como 0.30000000000000004`
    

Para redondear resultados a un número fijo de decimales, podemos utilizar `.toFixed()`.

`console.log(resultado.toFixed(2)); // "0.30"`

## ¿Qué operaciones avanzadas podemos hacer con `Math`?

JavaScript brinda el objeto `Math` para operaciones matemáticas avanzadas:

- **Raíz cuadrada (`Math.sqrt`)**: Calcula la raíz cuadrada de un número.
    
    `let raizCuadrada = Math.sqrt(16); // 4`
    
- **Valor absoluto (`Math.abs`)**: Devuelve el valor absoluto de un número.
    
    `let valorAbsoluto = Math.abs(-7); // 7`
    
- **Número aleatorio (`Math.random`)**: Genera un número aleatorio entre 0 y 1.
    
    `let aleatorio = Math.random();`
    

El tipo de dato `number` en JavaScript es fundamental en el desarrollo de aplicaciones donde se requiere manejo de números y cálculos matemáticos, asegurando versatilidad y facilidad en su implementación.