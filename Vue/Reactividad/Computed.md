Las _computed properties_ en Vue son una de las tres formas de manejar reactividad y la opción ideal cuando necesitas valores derivados que se recalculen solo cuando cambian sus dependencias. Si ya conoces _ref_, este recurso te ayudará a optimizar el rendimiento de tus componentes sin sacrificar reactividad.

## ¿Qué hace computed en Vue y por qué importa?

Una _computed property_ envuelve el retorno de una función y crea una propiedad reactiva computada. Cada vez que cambian las variables que están dentro del cuerpo de esa función, Vue vuelve a calcular el valor en el render.

La diferencia frente a un estado tradicional con _ref_ es clave: aunque ambas son reactivas, las propiedades computadas son cacheables. Es decir, si el valor calculado sigue siendo el mismo, Vue no lo recalcula y lo mantiene constante. Eso reduce _re-renders_ innecesarios y mejora el _performance_.

> **¿Qué significa que una computed property sea cacheable?** Que Vue guarda el último valor calculado y solo lo vuelve a calcular cuando alguna de sus dependencias reactivas cambia. Si nada cambió, devuelve el valor en caché.

## ¿Cómo se usa computed paso a paso?

Para crear una propiedad computada importas _computed_ desde Vue y le pasas siempre una función con el cálculo que quieres realizar . Dentro puedes hacer tres tipos de cálculos comunes:

- Reaccionar a cambios de estado, como el ancho de pantalla que muta constantemente.
- Operaciones de lógica booleana que devuelven un valor según verdadero o falso.
- Cálculos aritméticos basados en otras variables reactivas.

### Ejemplo práctico con styleButton

En la clase se construye una variable llamada _styleButton_ que cambia el color de los botones a rojo cuando ganas el juego. La función hace un _return_ condicional: si _win.value_ es verdadero, devuelve `background: red`; si no, devuelve un estilo vacío.

```js 
const styleButton = computed(() => { 
	if (win.value) { 
		return { background: 'red' } 
	} return {} 
})
```
Luego se aplica con un _bind_ de estilo en los botones del template y, al llegar al número que hay que adivinar (en el ejemplo, el cinco), además de soltar el confeti, los botones cambian a rojo .

### Cómo inspeccionar una computed property

Al recargar la página y abrir las herramientas de Vue, _styleButton_ aparece dentro del _setup_ como propiedad computada. En el DOM, los botones tienen el atributo _style_ vacío hasta que se cumple la condición y entonces se pinta el color.

> **¿Cuándo conviene usar computed en vez de escribir lógica en el template?** Siempre que tengas un cálculo fijo. Si lo escribes en el template, se ejecuta en cada render. Con computed, solo se recalcula cuando cambian sus dependencias.

## ¿Por qué computed mejora el performance de tu aplicación?

Cuando pones la lógica directamente en el template, Vue ejecuta ese cálculo en cada render del componente. Con una _computed property_, el cálculo solo corre si cambia una dependencia. En el ejemplo del contador, el valor era un objeto vacío la mayoría del tiempo y solo mutaba al ganar.

Esto parece poco en un juego pequeño, pero escala fuerte en aplicaciones con cientos de componentes. Usar _computed_ de forma responsable ayuda a reducir:

- Tiempos de _re-render_ en páginas con mucha interactividad.
- _Bundle size_ y carga de cómputo en cada actualización.
- Cuellos de botella en aplicaciones que manejan millones de clientes.

La recomendación final es clara: cada vez que tengas un valor derivado de otros datos reactivos, envuélvelo en una _computed property_ en lugar de calcularlo dentro del template. Así aprovechas el caché interno de Vue y mantienes tu interfaz fluida.