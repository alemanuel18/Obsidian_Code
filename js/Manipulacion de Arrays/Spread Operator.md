Dominar el **spread operator** en JavaScript abre la puerta a manipular arrays de forma limpia, segura y expresiva. Con solo tres puntos (`...`) puedes copiar arrays sin mutar los originales, combinar varios en uno solo, crear nuevos arrays con elementos adicionales e incluso pasar valores directamente como parámetros de una función.

## ¿Cómo copiar un array sin modificar el original?

Una de las ventajas principales del _spread operator_ es generar **copias independientes** de un array. Esto resulta fundamental cuando necesitas trabajar con datos sin alterar la fuente original, algo conocido como evitar la **mutación** de valores .

![[Pasted image 20260611105646.png]]
![[Pasted image 20260611105710.png]]
Al usar `[...originalArray]`, cada elemento se despliega dentro de un nuevo array. Cualquier cambio que hagas en `copyOfArray` **no afectará** al array original. Esta técnica es muy útil en proyectos donde la **inmutabilidad** de los datos es una prioridad.

## ¿Cómo combinar arrays y agregar elementos extra?

Otra aplicación muy práctica es la **combinación de arrays**. En lugar de recurrir a métodos como `concat`, el _spread operator_ ofrece una sintaxis más clara y directa .

![[Pasted image 20260611105748.png]]

## ¿Se pueden crear arrays con elementos adicionales a partir de uno existente?

Sí. Puedes tomar un array como base y añadirle nuevos valores en la misma declaración, sin tocar el original .

![[Pasted image 20260611105851.png]]

Esta estrategia es especialmente útil cuando construyes listas dinámicas: partes de un conjunto conocido y le sumas elementos según lo necesites.

## ¿Cómo pasar elementos de un array como parámetros de una función?

El _spread operator_ también resuelve un escenario muy común: tienes los valores almacenados en un array, pero la función espera **parámetros individuales** .

![[Pasted image 20260611110022.png]]

## ¿Qué sucede internamente al usar spread en la llamada?

Al escribir `sum(...numbers)`, JavaScript **despliega** cada elemento del array y lo asigna en orden a los parámetros `a`, `b` y `c`. Es equivalente a escribir `sum(1, 2, 3)`, pero con la ventaja de que los valores provienen de una estructura dinámica. Antes del _spread operator_, esto se lograba con `Function.prototype.apply`, una alternativa mucho menos legible.

En resumen, las cuatro formas principales de aprovechar este operador son:

- **Copiar** un array para proteger los datos originales.
- **Combinar** dos o más arrays en uno solo.
- **Crear** nuevos arrays agregando elementos a uno existente.
- **Pasar** elementos de un array como argumentos de función.