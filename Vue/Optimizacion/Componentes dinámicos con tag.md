Cambiar un componente completo en lugar de mutar el DOM es una de las funcionalidades más potentes de Vue. Con los **componentes dinámicos** puedes desmontar uno y montar otro de forma automática según una condición, ideal para escenarios como galerías de íconos o vistas que rotan.

## ¿Qué son los componentes dinámicos en Vue?

Son componentes que se intercambian en tiempo de ejecución sin tener que escribir múltiples bloques condicionales. En vez de declarar cada componente por separado, defines un único punto de renderizado que cambia según el valor que le pases.

Imagina que entras a una empresa y te encuentras una carpeta con cientos de íconos. Importarlos uno por uno funciona, pero crear un componente _icon_ que reciba un parámetro y renderice el ícono correcto es mucho más escalable. Ese es exactamente el caso de uso donde brillan los componentes dinámicos.

> **¿Para qué sirven los componentes dinámicos en Vue?** Sirven para reemplazar un componente completo por otro en tiempo de ejecución, sin reescribir lógica condicional. Útiles en galerías de íconos, _tabs_, _wizards_ o vistas que rotan según el estado.

## ¿Cómo se usa la tag component con el atributo is?

Vue ofrece una etiqueta especial llamada _component_ que recibe el atributo _is_. Ese atributo le indica qué renderizar en ese punto del template.

El atributo _is_ puede recibir directamente una tag HTML como string, por ejemplo _span_, y Vue la renderizará tal cual. Sin embargo, esa forma es poco habitual y el propio editor sugiere usar _v-bind_ para que el valor sea dinámico.

### La forma recomendada se ve así:

```vue 
<component :is="icons.left" />
```

Donde _icons_ es un objeto que actúa como diccionario:

```js 
const icons = { left: ChevronLeft, right: ChevronRight, }
```

Con ese patrón, cambiar de ícono es tan simple como cambiar la clave: _icons.left_ o _icons.right_. Si pones _left_ en ambos botones, verás las dos flechas apuntando al mismo lado, prueba clara de que el componente se está resolviendo dinámicamente.

## ¿Por qué necesitas v-bind en el atributo is?

Porque sin _v-bind_, Vue interpreta el valor como string y espera una tag HTML literal. Con _v-bind_ (o su forma corta `:is`), Vue evalúa la expresión y resuelve la referencia al componente importado. Es la diferencia entre pasar el texto _"ChevronLeft"_ y pasar el componente real.

## ¿Qué pasa con el ciclo de vida al cambiar un componente dinámico?

Aquí viene la parte que debes tener muy presente. La tag _component_ **desmonta y monta el componente cada vez que cambia el valor de is**. No es un simple intercambio visual: es una destrucción y recreación completa.

Eso significa que todo el ciclo de vida vuelve a ejecutarse:

- El componente sale del _Shadow DOM_ que maneja Vue.
- Se dispara _unmounted_ en el componente saliente.
- Se dispara _mounted_ en el componente entrante.
- Cualquier cálculo o efecto, como una llamada a una API, se vuelve a ejecutar.

> **¿Los componentes dinámicos preservan su estado al cambiar?** No. Al cambiar el valor de _is_, Vue desmonta el componente actual y monta el nuevo, reiniciando estado interno y efectos del ciclo de vida.

Esto puede ser justo lo que quieres, por ejemplo cuando necesitas refrescar datos cada vez que cambias de vista. Pero también puede ser un problema si tu componente hace _fetch_ costoso o guarda estado local que no debería perderse.

## ¿Cuándo conviene usar componentes dinámicos y cuándo no?

Úsalos cuando:

- Tienes una colección de componentes intercambiables, como íconos o _tabs_.
- El remontaje no afecta el rendimiento ni la experiencia.
- Quieres lógica limpia sin cadenas de _v-if_.

Evítalos o combínalos con _KeepAlive_ cuando:

- El componente hace llamadas a API que no deben repetirse en cada cambio.
- Necesitas preservar estado interno entre cambios.
- El costo de remontar es alto.

El patrón de diccionario más _component :is_ te abre la puerta a interfaces más flexibles. Cuéntame en los comentarios qué caso de uso piensas resolver primero con componentes dinámicos en tu proyecto.