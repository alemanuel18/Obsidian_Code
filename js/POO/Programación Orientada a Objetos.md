Entender qué es un objeto en JavaScript es el primer paso para dominar uno de los paradigmas más importantes de la programación moderna. Un objeto es, en esencia, una **estructura de datos** que almacena información mediante pares de **propiedad y valor** (_key value_), y que además puede contener funciones internas llamadas **métodos** para generar interacciones. A continuación se explica cómo construir objetos, anidarlos y dotarlos de comportamiento.

## ¿Qué es un objeto y cómo se estructura?

Un objeto se define con un nombre, se abren llaves y dentro se colocan las propiedades separadas por comas. Cada propiedad sigue el formato **propiedad: valor** . El valor respeta el tipo de dato que le corresponde: un _string_ va entre comillas y un número se escribe directamente.

La idea central detrás de los objetos es **abstraer la realidad y llevarla a programación** . Esto significa tomar elementos del mundo real —una persona, un automóvil, un producto— y representarlos con propiedades y valores que los describan. De ahí nace lo que se conoce como **programación orientada a objetos**, un paradigma que utiliza estas estructuras como base para modelar cualquier entidad.

## ¿Cómo se crea un objeto persona paso a paso?

Para ilustrar la idea, se construye una constante llamada `persona` :

javascript const persona = { nombre: "John", edad: 30, direccion: { calle: "Avenida Insurgentes 187", ciudad: "Ciudad de México" }, saludar: function () { console.log("Hola, mi nombre es " + persona.nombre); } };

- **nombre** es un _string_ que identifica a la persona.
- **edad** es un número que representa los años.
- **direccion** es un objeto anidado con sus propias propiedades.
- **saludar** es un método que ejecuta una acción.

## ¿Qué son los objetos anidados?

Dentro de un objeto, el valor de una propiedad puede ser **otro objeto** . En el ejemplo, `direccion` no es un texto simple sino una estructura con `calle` y `ciudad`. Esto permite organizar información compleja de forma jerárquica y legible, reflejando mejor cómo se relacionan los datos en el mundo real.

## ¿Cuál es la diferencia entre propiedades y métodos?

Las **propiedades** almacenan información estática: el nombre, la edad, la dirección. Son datos que describen al objeto. Los **métodos**, en cambio, son funciones que viven dentro del objeto y definen las **acciones** que este puede realizar .

En el ejemplo, `saludar` es un método porque ejecuta un comportamiento: imprime un mensaje que incluye el nombre del objeto. Para acceder a una propiedad desde el propio objeto se utiliza la **notación de punto** (`persona.nombre`), que indica que se está leyendo el valor `nombre` que pertenece al objeto `persona` .

- Las propiedades responden a la pregunta: **¿qué tiene este objeto?**
- Los métodos responden a la pregunta: **¿qué puede hacer este objeto?**

## ¿Por qué los objetos son fundamentales en JavaScript?

Los objetos están en todas partes: desde el formato **JSON** (_JavaScript Object Notation_) que se usa para intercambiar datos entre servidores y aplicaciones, hasta los componentes de cualquier _framework_ moderno. Comprender su estructura de _key value_, saber anidar objetos y definir métodos es la base sobre la que se construyen patrones más avanzados.

Cuando logras abstraer algo tan cotidiano como una persona y representarlo con propiedades como `nombre`, `edad` y `direccion`, y con métodos como `saludar`, ya estás aplicando el pensamiento de la **programación orientada a objetos**. Este ejercicio de abstracción es lo que permite modelar sistemas completos a partir de entidades simples y reutilizables.