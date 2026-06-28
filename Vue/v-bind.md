El verdadero superpoder de Vue está en combinar JavaScript con nodos de HTML usando una sintaxis específica. Aprenderás a interpolar variables, atar atributos dinámicos y entender por qué la **directiva v-bind** es clave cuando trabajas con atributos HTML dentro de tus componentes.

Este recurso es para quienes ya saben declarar un componente en Vue y quieren dar el siguiente paso: hacer que el HTML responda a valores definidos en JavaScript.

## ¿Cómo preparo el proyecto antes de escribir sintaxis Vue?

Antes de tocar JavaScript, conviene partir de una base con estilos ya listos para enfocarte solo en la lógica.

Desde la terminal, dentro del repositorio del curso, cámbiate de la rama main a la rama de trabajo con `git checkout vue-syntax-start` . Esa rama trae varios cambios listos: un color global para la fuente, una nueva estructura del componente _game-counter_, clases CSS para los botones y un _wrapper_ dentro de un main en el componente app.

Al correr la aplicación verás los estilos aplicados, pero la funcionalidad sigue siendo la misma que ya conocías. El siguiente paso es atar esos elementos a variables de JavaScript.

## ¿Qué es la reactividad y cómo se usa la sintaxis de bigote en Vue?

La **reactividad** es la capacidad de que un valor en pantalla cambie automáticamente cuando cambia su variable asociada. Es justamente lo que distingue a Vue de un HTML estático.

Dentro del componente _game-counter_, puedes declarar una variable llamada `number` con un valor inicial, por ejemplo 10 . Para mostrar esa variable dentro de una etiqueta, Vue usa una sintaxis especial llamada _mustache wrapper_ o envolvente de bigote, que se escribe con dobles corchetes.

> **¿Qué es el mustache wrapper en Vue?** Es la sintaxis de dobles llaves `{{ }}` que permite interpolar variables o funciones de JavaScript dentro del texto de una etiqueta HTML de forma segura.

La forma de usarlo es simple: escribes el nombre de la variable entre los dobles corchetes y Vue se encarga de pintar su valor. Si cambias el número a 100 o 1.000, el valor se actualiza en automático en la vista. Aún no es reactividad completa (eso llega más adelante en el curso), pero ya estás inyectando JavaScript de manera segura dentro del template.

## ¿Puedo invocar funciones dentro de los dobles corchetes?

Sí. Si una función devuelve un string o un número, basta con invocarla dentro de las llaves, igual que harías con una variable. Esto te da flexibilidad para mostrar resultados calculados sin ensuciar el HTML con lógica adicional.

## ¿Cómo uso v-bind para atributos dinámicos en Vue?

Aquí viene una distinción clave: los dobles corchetes funcionan para el **texto interno** de una etiqueta, no para sus **atributos**. Si intentas poner `id="{{ id }}"` vas a tener un error.

Para inyectar JavaScript en un atributo HTML necesitas la **directiva v-bind**. La sintaxis corta es solo dos puntos seguidos del nombre del atributo .

```html 
<span :id="id">{{ number }}</span>
```
De esta forma, si declaras una variable `id` con un `Math.random()`, cada recarga generará un identificador aleatorio en el span. La regla práctica es directa:

- Si vas a inyectar valor en el **texto** de una etiqueta, usa dobles corchetes.
- Si vas a inyectar valor en un **atributo** HTML, usa v-bind con dos puntos.
- Si la función devuelve un valor, puedes invocarla en cualquiera de los dos contextos.

> **¿Cuándo debo usar v-bind en lugar de dobles corchetes?** Siempre que quieras controlar el valor de un atributo HTML como id, class, aria-label o cualquier otro. Los dobles corchetes solo funcionan en el contenido de texto.

## ¿Cómo interpolo el nombre del atributo en Vue?

Vue permite algo aún más potente: interpolar incluso el **nombre** del atributo, no solo su valor. Para eso usas corchetes cuadrados dentro del v-bind.

Imagina que defines dos variables: `myAttr` con el valor `"aria-label"` y `ariaLabelValue` con el texto `"número del contador"` . La sintaxis queda así:

```html 
<span :[myAttr]="ariaLabelValue">{{ number }}</span>
```

Al recargar, el span renderizará `aria-label="número del contador"`. Si el atributo no aparece, revisa por _typos_ en los nombres de variables; un error común es escribir mal una palabra y que Vue marque la variable como nunca usada.

## ¿Qué puedes hacer con la sintaxis dinámica de Vue?

Con lo que ya viste, puedes resolver muchos casos prácticos sin escribir lógica compleja:

- Mostrar variables de JavaScript dentro del texto de cualquier etiqueta.
- Llamar funciones que devuelven strings o números directamente en el template.
- Asignar valores dinámicos a atributos HTML como id, class o aria-label con v-bind.
- Cambiar incluso el nombre del atributo de forma dinámica usando corchetes.

La regla mental que te conviene grabar: **texto interno con dobles corchetes, atributos con v-bind**. Esa diferencia te ahorra horas de debugging.

El siguiente paso natural son las propiedades de los componentes, también conocidas como _props_, que permiten pasar información de un componente padre a un componente hijo.