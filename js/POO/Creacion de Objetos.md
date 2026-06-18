

Los objetos en programación son estructuras de datos que permiten almacenar información de una manera organizada. Funcionan con una estructura de clave-valor, donde cada clave (key) se asocia a un valor (value), lo que nos ayuda a mantener una colección de datos relacionados de forma coherente.

Los objetos no solo almacenan datos, también pueden contener métodos que son acciones ejecutables por el propio objeto. Esta capacidad para almacenar tanto datos como comportamientos hace que los objetos sean herramientas versátiles y poderosas en muchos lenguajes de programación.

## ¿Cómo crear un objeto en JavaScript?

Crear un objeto en JavaScript comienza declarando una constante y usando llaves para definir las propiedades y métodos dentro del objeto. Aquí te muestro cómo:

![[Pasted image 20260611142430.png]]

En este ejemplo, hemos creado un objeto llamado `persona` con propiedades como `nombre`, `edad` y `direccion`. Además, el método `saludar` imprime un mensaje utilizando la propiedad `nombre`.

## ¿Cómo trabajar con métodos de objetos?

Los métodos en un objeto se crean como funciones dentro del mismo. Estos métodos permiten que el objeto realice acciones usando sus propias propiedades.

Para ejecutar el método `saludar` del objeto `persona`, simplemente llamamos:

![[Pasted image 20260611142441.png]]

Este código ejecuta la acción definida en el método `saludar`, mostrando el saludo con el nombre de la persona.

## ¿Cómo agregar y borrar propiedades y métodos?

Agregar propiedades y métodos

Agregar nuevas propiedades o métodos a un objeto existente es sencillo. Solo necesitas utilizar el operador de punto (`.`) seguido del nombre de la nueva propiedad o método:

![[Pasted image 20260611142453.png]]

Borrar propiedades y métodos

Para eliminar una propiedad o método de un objeto, utiliza la palabra clave `delete`:

![[Pasted image 20260611142504.png]]

Con esto, las propiedades o métodos se eliminan del objeto, y ya no estarán accesibles.

---

Los objetos son fundamentales en muchos paradigmas de programación, especialmente en paradigmas orientados a objetos. Te permiten crear modelos del mundo real en el código, manejando tanto datos como funcionalidades. Recuerda que como programador, el dominio de los objetos y sus manipulaciones abre la puerta a desarrollar aplicaciones más completas y robustas. ¡Sigue explorando y experimentando para fortalecer tus habilidades!