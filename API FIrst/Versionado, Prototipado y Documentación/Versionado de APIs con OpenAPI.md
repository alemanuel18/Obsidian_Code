El versionado de APIs es la práctica que te permite evolucionar tu producto sin dejar tirados a los usuarios que ya consumen tu servicio. Cuando diseñas una API pensando en su crecimiento, necesitas garantizar que los nuevos cambios convivan con las implementaciones anteriores, y eso se logra configurando múltiples versiones tanto en tu archivo _OpenAPI_ como en la lógica de tu servidor.

## ¿Por qué necesitas versionar tu API desde el inicio?

Toda API que se mantiene viva tarde o temprano da un salto evolutivo. Agregar campos nuevos, cambiar tipos de datos o ajustar estructuras puede romper a los clientes que ya consumen tu servicio, y ahí es donde entra el versionado como red de seguridad.

Imagina que un endpoint devolvía un valor _string_ y ahora necesitas que sea numérico. Ese cambio aparentemente menor puede tumbar validaciones en el _front-end_ o en cualquier integración que dependa del tipo original. Por eso conviene exponer **v1** y **v2** en paralelo: los usuarios actuales siguen funcionando con la versión que ya conocen y los nuevos consumen las características recientes a su propio ritmo.

> **¿Qué es el versionado de una API?** Es la práctica de mantener varias versiones funcionales de tu API al mismo tiempo, identificadas como v1, v2, etc., para que los cambios nuevos no rompan a los clientes que usan versiones anteriores.

## ¿Cómo se configuran múltiples versiones en OpenAPI?

La configuración empieza en el archivo _OpenAPI_, dentro de la propiedad `servers`. Ahí defines cada versión con su URL y una descripción que explique qué hace cada una.

El flujo concreto que sigues es este:

- Abres el archivo _OpenAPI_ y localizas la sección `servers`.
- Defines la primera entrada apuntando a `v1` con una descripción como "versión uno de la API".
- Agregas una segunda URL apuntando a `v2` con su propia descripción.
- Mantienes el resto del documento intacto si los esquemas no cambian todavía.

La descripción de cada versión debería ser lo más clara posible. No basta con poner "v1" o "v2": indica qué incorpora, qué deprecó o qué corrigió, porque esa documentación es lo que tus consumidores leerán primero.

## ¿Y cómo refleja esto el archivo index del servidor?

En el archivo `index` del proyecto, expones cada versión como una ruta independiente. La **v1** queda igual que estaba, sirviendo el recurso original sin cambios, y la **v2** se monta como un nuevo `app.get` con la lógica mejorada.

Por ejemplo, si en `v1` el endpoint `/hello` devuelve un saludo simple, en `v2` puedes devolver el mismo saludo más un _timestamp_ y un mensaje adicional. Ambas rutas conviven en el mismo servidor y responden de forma independiente.

Un `console.log` con la información de cada versión y su ruta de documentación te ayuda a identificar rápidamente qué está corriendo cuando levantas el servidor con `npm run dev`.

## ¿Qué pasa con los usuarios cuando lanzas una nueva versión?

La idea central del versionado es la **migración gradual**. Nadie está obligado a moverse de inmediato a la versión nueva, y eso es justamente lo que protege tu producto.

Los usuarios que aún no migran siguen consumiendo `v1` sin notar diferencias. Los que ya están listos para las nuevas características apuntan a `v2` y aprovechan los datos extra. Y aquí viene lo interesante: muchas veces los campos nuevos son simplemente ignorados por implementaciones antiguas y no rompen nada, pero un cambio de tipo o de estructura sí lo haría. Por eso separar las versiones es tu seguro.

> **¿Cuándo conviene crear una v2 en lugar de modificar la v1?** Cuando el cambio rompe compatibilidad: tipos de datos distintos, campos eliminados o estructuras reorganizadas. Si solo agregas información opcional, muchas veces puedes mantener la misma versión.

## ¿Cómo se prueba que ambas versiones funcionan?

Al ejecutar el servidor y abrir la documentación generada por _OpenAPI_, vas a ver un selector de `servers` con las opciones disponibles. Eliges **v1** o **v2** y la herramienta envía las peticiones a la URL correspondiente.

Probando el endpoint `/hello` en ambas versiones, el resultado cambia: la v1 responde con el saludo original y la v2 responde con el saludo, el mensaje "versión dos" y el _timestamp_. Esa diferencia visible confirma que el versionado está funcionando como esperas.

## Conceptos clave que aparecen en la clase

Durante la implementación se tocan varias piezas que conviene tener claras:

- **OpenAPI** : especificación que describe tu API en un archivo declarativo, incluyendo la sección `servers` donde defines las versiones.
- **servers** : bloque del archivo _OpenAPI_ donde declaras las URLs de cada versión y sus descripciones.
- **Migración gradual** : estrategia que permite a los consumidores moverse de una versión a otra sin presión inmediata.
- **Compatibilidad de tipos de datos** : punto crítico donde un cambio de _string_ a número puede romper integraciones existentes.
- **npm run dev** : comando que levanta el servidor local para validar que ambas versiones responden correctamente.

Definir versiones desde el principio te da espacio para crecer sin miedo.