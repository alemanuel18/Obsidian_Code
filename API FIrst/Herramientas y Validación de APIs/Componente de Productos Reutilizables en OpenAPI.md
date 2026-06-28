Diseñar un esquema reutilizable en OpenAPI te permite estandarizar la estructura de tus datos, reducir repeticiones y validar campos antes de escribir una sola línea de código. Aquí aprenderás a construir un _schema_ de producto dentro de la sección `components`, aplicando tipos de datos, validaciones y reglas que luego podrás invocar desde cualquier _endpoint_ de tu API.

## Por qué usar components en OpenAPI

La sección `components` actúa como una biblioteca central donde defines una vez y reutilizas en todos los _paths_ y respuestas de tu documento.

En lugar de repetir la misma estructura en cada solicitud, defines un esquema base y lo referencias. Eso simplifica el mantenimiento y evita inconsistencias cuando tu API crece.

> **¿Qué son los components en OpenAPI?** Son bloques reutilizables que centralizan esquemas, respuestas y parámetros para que puedas invocarlos desde distintos _endpoints_ sin duplicar código.

## Cómo definir el esquema base de un producto

Antes de escribir el esquema conviene sentarse a diseñar: qué campos tendrá el producto, cuáles son obligatorios y qué validaciones aplican a cada uno .

El esquema arranca con el nombre `products`, el tipo `object` y un bloque `required` que marca los campos obligatorios:

- `name`: identifica el producto.
- `price`: define el valor monetario.
- `category`: clasifica el producto dentro de un grupo.

```yaml 
products: 
	type: object 
	required: 
		- name 
		- price 
		- category 
	properties: ...
```
Esto no significa que el producto solo tenga tres campos. Significa que sin esos tres, el producto no es válido.

## Cómo aplicar validaciones a strings y números

Cada propiedad necesita su tipo y sus reglas. Para `name` defines `type: string` con `minLength: 2` y `maxLength: 40`, evitando nombres demasiado cortos o exageradamente largos.

Para analizar ese máximo puedes apoyarte en una inteligencia artificial que revise tu catálogo y te sugiera el promedio real de caracteres .

En `description` usas un `string` con `maxLength` más generoso, entre 200 y 500 caracteres, porque ahí describes el producto a fondo.

Para `price` el tipo es `number` con dos reglas clave:

- `minimum: 0` para no permitir precios negativos.
- `multipleOf: 0.01` para garantizar dos decimales.

```yaml 
price: 
	type: number 
	minimum: 0 
	multipleOf: 0.01
```

## Cómo restringir valores con enum y arrays

La propiedad `category` es un `string` con valores predefinidos usando `enum`. Así limitas las opciones a un grupo cerrado:

```yaml 
category: 
	type: string 
	enum: 
		[
		"electronics",
		"books",
		"ropa",
		"food"
		]
```

Para `tags` defines un `array` cuyos `items` son `string`, con `minItems: 1`. La regla obliga a que cada producto tenga al menos una etiqueta .

> **¿Cómo se valida un array en OpenAPI?** Defines `type: array`, especificas el tipo de los `items` y agregas reglas como `minItems` o `maxItems` para controlar cuántos elementos acepta.

## Cómo manejar booleanos, objetos dinámicos y arrays anidados

No todos los campos siguen el mismo patrón. Algunos necesitan flexibilidad, otros estructura estricta.

Booleanos y objetos con propiedades dinámicas

El campo `inStock` se resuelve con un simple `type: boolean`. Existe o no existe stock, sin más matices.

Para `specifications` el reto es distinto: cada producto puede tener atributos técnicos diferentes. Aquí entra `additionalProperties`:

```yaml 
specifications: 
	type: object 
	additionalProperties: 
		type: string
```
Eso permite que el objeto acepte cualquier clave adicional siempre que su valor sea un _string_. Cuida la ortografía al escribirlo, porque un _typo_ rompe la validación.

## Arrays de objetos para reseñas

Las calificaciones requieren una estructura más compleja: un _array_ donde cada ítem es un objeto con sus propios campos obligatorios.

```yaml 
ratings: 
	type: array 
	items: type: object 
	required: 
		- score 
		- comment 
	properties: 
		score: 
			type: integer 
			minimum: 1 
			maximum: 5 
		comment: 
			type: string 
			maxLength: 200
```

El `score` se restringe a un `integer` entre 1 y 5. El `comment` es un `string` con tope de 200 caracteres para mantener las reseñas concisas .

## Qué ganas al diseñar antes de codear

Llegar a este esquema implica una fase previa de diseño donde defines tipos, refinas valores requeridos y ajustas propiedades a casos de uso reales: rangos de precio, decimales monetarios, categorías cerradas, etiquetas mínimas, control de stock y estructura de reseñas.

Cada validación responde a una decisión de producto, no a una convención arbitraria. Por eso el contrato de tu API queda claro antes de tocar el código que lo implementa.

Con este esquema reutilizable listo, el siguiente paso es pedirle a una inteligencia artificial que actualice el documento OpenAPI usando esta estructura como base.