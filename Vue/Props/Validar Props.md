Validar props en Vue es la práctica de indicarle al framework qué tipo de dato esperas recibir en cada propiedad de un componente, si es obligatoria y qué valor tomar por defecto. Esta validación previene errores en aplicaciones reactivas y es clave cuando trabajas con datos externos como respuestas de APIs.

Aunque JavaScript no es un lenguaje fuertemente tipado y va infiriendo los tipos conforme interpreta el código, Vue te da herramientas para tipar tus props sin necesidad de migrar a _TypeScript_. Y aunque Vue se lleva muy bien con _TypeScript_, en JavaScript plano puedes lograr una validación robusta.

## ¿Cómo defines el tipo de dato de una prop en Vue?

En lugar de declarar tus props como un arreglo simple, conviértelas en un objeto de configuración donde cada propiedad recibe sus reglas. Vue trae por defecto soporte para tipos como _Number_, _String_, _Array_, _Object_ e incluso valores nulos .

Por ejemplo, si tu componente `GameCounter` recibe un `minNumber` y un `maxNumber`, puedes tiparlos así:

```js 
props: { 
	minNumber: { 
		type: Number, 
		required: true 
	}, 
	maxNumber: { 
		type: Number, 
		required: true 
	} 
}
```

La propiedad `type` define el tipo esperado y `required: true` obliga a que quien use el componente pase ese valor. Si no lo hace, verás en consola el warning _Missing required prop: minNumber_.

> **¿Qué pasa si no paso una prop marcada como required en Vue?** Vue no rompe la app, pero lanza un warning en consola indicando que falta la prop requerida. El componente intentará renderizar sin ese valor.

## ¿Cómo asignas un valor por defecto y aceptas múltiples tipos?

La propiedad `default` te permite definir un valor inicial cuando no se pasa la prop desde el componente padre. Por ejemplo, si pones `default: 0` en `maxNumber`, el componente renderizará con cero aunque no recibas nada .

Y si una prop puede llegar como número o como texto, declara el tipo como un arreglo:

```js 
example: { type: [Number, String] }
```

Esto es útil cuando consumes APIs como la de _Pokémon_ o _Rick and Morty_, donde no siempre tienes mapeados todos los casos de uso y los valores pueden variar de formato.

## ¿Cómo creas un validador personalizado para props?

Vue te permite agregar una función `validator` que recibe el valor de la prop como argumento y devuelve `true` o `false` según tus reglas. Esto va más allá del tipo de dato y te deja controlar qué valores específicos aceptas.

Un ejemplo concreto: imagina que tu prop `example` solo debe aceptar los strings `+` o `-`.

```js 
example: { 
	type: String, 
	validator: (value) => { return ['+', '-'].includes(value)} 
}
```

Si alguien pasa `"Hola"` como valor, Vue lanzará el warning _Custom validator check failed for prop example_. Pero si pasas `"+"`, todo pasa la validación sin problemas .

> **¿Para qué sirve un validator en una prop de Vue?** Sirve para restringir los valores aceptados más allá del tipo de dato. Por ejemplo, aceptar solo strings específicos, rangos numéricos o formatos concretos.

## ¿Cómo declaras arrays y objetos como valor por defecto?

Aquí viene una regla clave que confunde a muchos: cuando el `default` es un _array_ o un _object_, no puedes asignarlo directamente. Tienes que envolverlo en una función que retorne el valor.

La razón es que los objetos y arrays son referencias en JavaScript, y Vue necesita una nueva instancia para cada componente que use esa prop.

```js 
example: { type: Array, default: () => [1, 2, 3, 4] }
```

Para objetos funciona igual, pero recuerda usar paréntesis dentro de la _arrow function_ para que JavaScript no interprete las llaves como cuerpo de función:

```js 
example: { type: Object, default: () => ({ name: 'Enrique' }) }
```

Sin esos paréntesis externos, JavaScript leerá `{}` como bloque de código en vez de objeto literal y obtendrás un error de sintaxis .

## ¿Por qué validar props es fundamental en frameworks reactivos?

Validar propiedades te permite anticiparte a los errores en tiempo de desarrollo en lugar de depurarlos en producción. En aplicaciones reactivas, donde los datos fluyen entre múltiples componentes, saber con certeza qué tipo de valor llega a cada uno reduce drásticamente los bugs.

Esto cobra más importancia cuando consumes datos externos, porque las APIs no siempre devuelven estructuras predecibles. Tener una capa de validación en tus props funciona como un contrato entre componentes.

Las tres ventajas concretas que te da Vue al validar props son:

- Detectar props faltantes con `required: true`.
- Garantizar el tipo correcto con `type`.
- Restringir valores específicos con `validator`.

Ahora ponlo a prueba con tu propio `GameCounter`: piensa qué otras props podrías pasarle desde la aplicación principal. Un número aleatorio, una _flag_ para indicar si el jugador ganó, un contador de intentos.