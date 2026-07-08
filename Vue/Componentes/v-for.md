Renderizar listas en Vue se vuelve trivial cuando entiendes **v-for**, la directiva que itera sobre un arreglo y dibuja un mismo componente tantas veces como elementos haya. Aquí aprenderás a usarla con un caso real: renderizar varias _cards_ de juegos a partir de datos de una API, sin repetir código ni sacrificar _performance_.

## ¿Qué hace la directiva v-for en Vue?

La directiva v-for recorre un iterable (normalmente un arreglo) y crea un nodo del DOM por cada elemento. En lugar de declarar manualmente cinco veces el mismo componente, escribes la plantilla una sola vez y Vue la replica con la información de cada ítem.

En el ejemplo, partimos de un componente llamado GameCard que recibe una única propiedad: game. Ese objeto contiene title, description, galleryImages, tags y publicationYear. Si solo quisiéramos pintar el primer juego, bastaría con pasarle state.data[0] y listo. Pero cuando hablamos de cinco, cien o mil juegos, hardcodear índices deja de ser viable.

> **¿Qué es v-for en Vue?** Es una directiva que itera sobre un arreglo y renderiza un componente o elemento por cada ítem, usando una sintaxis tipo `item in lista`.

## ¿Cómo se escribe la sintaxis de v-for con un arreglo?

La estructura básica se parece a un bucle de Python, aunque internamente es JavaScript puro. Sobre el componente que quieres repetir, agregas la directiva con dos piezas obligatorias.

- El iterable y la variable temporal: `v-for="game in state.data"`.
- La propiedad **:key** con un valor único por elemento, por ejemplo `:key="game.title"`.
- La prop que pasas al componente, en este caso `:game="game"`.

Con eso, cada GameCard recibe su propio objeto game y se renderiza con su galería, su título y sus tags. La aplicación pasa de mostrar una _card_ rota o repetida a mostrar la lista completa con una sola línea de plantilla.

## ¿Por qué v-for necesita una key única?

Vue usa la **key** para identificar cada nodo dentro del DOM virtual. Si tuvieras múltiples nodos iguales aunque con información distinta, Vue tendría problemas para saber cuál actualizar, cuál mover y cuál destruir cuando cambia la lista.

La recomendación es usar un identificador realmente único: un id de base de datos suele ser mejor que un title, porque dos juegos podrían compartir nombre. En el ejemplo se usa game.title porque sabemos que no se repite, pero en producción conviene apoyarse en un id estable.

> **¿Para qué sirve la prop key en v-for?** Le da a Vue una huella única por elemento para que pueda diferenciar nodos similares en el DOM y actualizar solo lo necesario cuando la lista cambia.

## ¿Cuándo conviene evitar anidar v-for por performance?

Un v-for es, en esencia, un for de JavaScript. Si anidas varios, multiplicas el trabajo de renderizado. En el ejemplo hay un v-for doble sin que se note: el primero recorre las _cards_ de juegos y el segundo, dentro de GameCard, recorre las tags de cada juego.

Con pocos elementos no hay problema. Pero imagina renderizar tags para 10.000 usuarios sin paginación: el navegador se arrastraría. Algunas prácticas para mantener el _performance_ sano:

1. Pagina o aplica _scroll_ virtual cuando la lista sea grande.
2. Evita anidar v-for sobre estructuras profundas si puedes aplanar los datos.
3. Usa keys estables (no índices del arreglo) para que Vue reutilice nodos en lugar de recrearlos.

Y aquí viene lo interesante: muchas veces el cuello de botella no es Vue, sino la cantidad de componentes con animaciones o reactividad que estás pintando al mismo tiempo. Medir antes de optimizar siempre paga.

## ¿Qué conceptos clave aprendiste sobre v-for?

La directiva v-for te permite iterar un arreglo y renderizar el mismo componente varias veces, lo cual es ideal cuando los datos vienen de una API. El componente GameCard recibe una prop game con title, description, galleryImages, tags y publicationYear, y al combinarlo con v-for basta una línea para pintar toda la galería.

La propiedad key es obligatoria porque Vue la usa para distinguir nodos únicos en el DOM virtual y actualizar la vista sin errores. La sintaxis `game in state.data` recuerda a Python pero es JavaScript, y la prop game viaja del padre al hijo en cada iteración.

Finalmente, el **performance** importa: anidar v-for replica trabajo, así que cuida la profundidad de tus iteraciones cuando tengas listas grandes o componentes con animaciones.