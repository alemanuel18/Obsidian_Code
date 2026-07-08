Trabajar con frameworks reactivos como Vue, React o Angular exige algo más que dominar la sintaxis: necesitas un **pensamiento dirigido a componentes**. Esa mentalidad te permite dividir una interfaz en piezas pequeñas y reutilizables, declararlas una sola vez y usarlas en toda la aplicación.

## ¿Qué es el pensamiento por componentes en Vue?

Es la práctica de mirar cualquier pantalla, layout o respuesta de una API y descomponerla en bloques con una única responsabilidad. En lugar de escribir un botón cinco veces, lo defines una vez y lo reutilizas donde haga falta.

> **¿Qué significa pensar en componentes?** Significa identificar la mínima unidad reutilizable de tu UI (un botón, un título, una _tag_) y construirla como pieza independiente para usarla en múltiples lugares.

La ventaja práctica es directa: menos código duplicado, mantenimiento más fácil y una app que escala sin volverse un caos.

## ¿Cómo dividir una card de videojuego en componentes reutilizables?

En el segundo proyecto del curso vas a consumir la API **Game Stream**, que devuelve información de varios videojuegos. Cada juego llega con un montón de datos y, a primera vista, parece un solo bloque. Aquí viene lo interesante: ese bloque se puede partir en piezas más chicas.

Mirando una _card_ típica, puedes identificar estas responsabilidades:

- **Header**: título, subtítulo, estudio y año de publicación.
- **Video**: el reproductor o preview del juego.
- **Plataformas**: las _tags_ que indican dónde está disponible.
- **Descripción**: el bloque de información del juego.
- **Galería**: el conjunto de imágenes.

Cada uno de esos bloques se convierte en un componente independiente. Los declaras una vez y los reutilizas en cada juego que la API devuelva.

## ¿Por qué dividir hasta la mínima responsabilidad?

Porque mientras más pequeño y específico sea un componente, más fácil es reutilizarlo. Un componente _Tag_ sirve para plataformas hoy y mañana puede servir para géneros, etiquetas de descuento o estados de stock.

> **¿Cuál es la mínima responsabilidad de un componente?** Hacer una sola cosa bien: mostrar un título, renderizar una imagen, listar plataformas. Si un componente hace dos cosas distintas, probablemente deba dividirse.

Esta regla aplica igual cuando trabajas con datos de una API que cuando recibes un diseño de Figma en tu trabajo.

## ¿Por qué Vue, React y Angular comparten esta filosofía?

Los tres frameworks parten de la misma idea: una **arquitectura modular y reactiva**. Tú declaras un componente con su lógica, su template y sus estilos, y el framework se encarga de renderizarlo cada vez que lo invoques con datos distintos.

En el proyecto vas a ver esto en acción: la API devuelve varios juegos, pero tú solo declaras los componentes una vez. El framework los repite por cada _item_ que llega en la respuesta.

## ¿Cómo aplicar este enfoque a cualquier layout?

Antes de escribir código, observa el diseño y hazte tres preguntas:

1. ¿Qué partes se repiten visualmente?
2. ¿Qué bloques tienen una sola responsabilidad clara?
3. ¿Qué piezas podrían reutilizarse en otra pantalla?