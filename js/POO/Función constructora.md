Crear objetos de forma manual está bien cuando necesitas uno o dos, pero cuando el proyecto exige cientos de ellos, copiar y pegar deja de ser una opción viable. Las **funciones constructoras** en JavaScript resuelven exactamente ese problema: permiten fabricar objetos de manera escalable, reutilizable y organizada.

## ¿Cómo se crea una función constructora en JavaScript?

Una función constructora es, en esencia, una función cuyo único propósito es **construir objetos** . Su sintaxis es la misma que la de cualquier función, con dos diferencias importantes:

- El nombre de la función **inicia con mayúscula** (por convención). Si queremos crear personas, la función se llama `Persona`.
- Dentro del cuerpo se utiliza la palabra clave **`this`** para asignar cada propiedad al objeto que se está construyendo.

![[Pasted image 20260611143635.png]]
El **`this`** hace referencia al objeto concreto que se está creando en ese momento. Así, `this.nombre = nombre` significa: "la propiedad `nombre` de _este_ objeto será igual al parámetro que recibimos".

## ¿Qué es una instancia y cómo se genera?

Cada objeto que nace a partir de una función constructora recibe el nombre de **instancia** . Para crearla se usa la palabra reservada **`new`** seguida de la función constructora con sus argumentos:

![[Pasted image 20260611143708.png]]

`console.log(persona1);` // Persona { nombre: 'Juan', apellido: 'Pérez', edad: 30 } `console.log(persona2);` // Persona { nombre: 'Diego', apellido: 'De Granda', edad: 35 }

La ventaja es evidente: en lugar de duplicar bloques de código, solo invocas la función con los datos que cambian . Incluso podrías automatizar el proceso dentro de un ciclo para generar tantas instancias como necesites.

## ¿Para qué sirve prototype en una función constructora?

Después de definir la función constructora, es probable que necesites **agregar nuevas propiedades o métodos** sin modificar el constructor original. Aquí entra en juego el **prototype** .

El _prototype_ es un objeto especial que actúa como una copia compartida de la función constructora. Todo lo que agregues al prototype estará disponible para **todas las instancias**, presentes y futuras.

`Persona.prototype.telefono = '555-555-5555';`

Al inspeccionar cualquiera de las instancias, esta propiedad no aparece directamente en el objeto, sino dentro de su **prototipo** . JavaScript busca primero en el objeto; si no encuentra la propiedad, la busca en la cadena de prototipos.

## ¿Cómo agregar una propiedad solo a una instancia específica?

Si la nueva propiedad no necesita compartirse con las demás instancias, se asigna directamente sobre el objeto :

javascript persona1.nacionalidad = 'mexicano';

- `persona1` tendrá la propiedad `nacionalidad`.
- `persona2` **no** la tendrá, porque no se la asignamos.

Esto permite personalizar instancias individuales sin afectar al resto.

## ¿Cómo se agrega un método a través de prototype?

Los métodos también se añaden al _prototype_ para que todas las instancias los hereden . Se define como una función anónima asignada a la propiedad deseada:

javascript Persona.prototype.saludar = function () { console.log(`Hola, me llamo ${this.nombre} ${this.apellido}`); };

persona1.saludar(); // Hola, me llamo Juan Pérez persona2.saludar(); // Hola, me llamo Diego De Granda

Dentro del método, **`this`** vuelve a apuntar a la instancia que lo invoca, lo que permite acceder a sus propiedades particulares. Así, cada persona saluda con su propio nombre y apellido.

## ¿Cuándo conviene usar funciones constructoras frente a objetos literales?

La regla es sencilla:

- **Objeto literal** → cuando necesitas un solo objeto o unos pocos con estructuras diferentes.
- **Función constructora** → cuando vas a crear múltiples objetos con la misma estructura y quieres mantener el código limpio y escalable.

Combinar la función constructora con el _prototype_ te da la flexibilidad de extender la estructura en cualquier momento, ya sea con propiedades por defecto o con métodos que todas las instancias puedan utilizar. Si quieres profundizar más, prueba a crear tu propia función constructora y experimenta agregando propiedades y métodos tanto al constructor como al _prototype_. Comparte en los comentarios qué estructura diseñaste y qué resultados obtuviste.

![[Pasted image 20260611143859.png]]