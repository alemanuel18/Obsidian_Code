El módulo _Timers_ de Node.js te da una API global para programar funciones que se ejecutan en momentos específicos del ciclo de vida de tu aplicación. Si vienes del navegador, ya conoces nombres como `setTimeout` o `setInterval`, pero aquí funcionan distinto y entender esa diferencia te permite escribir código más predecible.

Esta guía te muestra cómo usar `setTimeout`, `setImmediate`, `setInterval` y sus respectivos cancelers (`clearTimeout`, `clearInterval`) dentro de un archivo `timers.js`, con ejemplos prácticos que puedes correr en tu terminal.

## ¿Qué hace el módulo Timers en Node.js?

El módulo _Timers_ expone funciones globales que te permiten **diferir, repetir o cancelar la ejecución de código** según el flujo del _event loop_. No necesitas importarlo: está disponible globalmente, igual que en el navegador, pero su comportamiento se acopla al ciclo de vida del runtime .

> **¿Qué es el módulo Timers?** Es una API global de Node.js que programa funciones para ejecutarse después de un tiempo, en la próxima iteración del bucle, o de forma repetida hasta que las canceles.

## ¿Cómo marco la hora actual para medir la ejecución?

Antes de programar timers, conviene imprimir un punto de referencia. Con `new Date().toLocaleTimeString()` capturas la hora exacta en que arranca el script:

```javascript 
console.log("hora actual", new Date().toLocaleTimeString());
```

Esto te da una línea base para comparar cuándo se disparan los mensajes diferidos frente a los síncronos.

## ¿Cuándo uso setTimeout, setImmediate o setInterval?

Cada función responde a una intención distinta. **`setTimeout` ejecuta una vez después de N milisegundos**, **`setImmediate` ejecuta en la próxima iteración del bucle**, y **`setInterval` repite la ejecución cada N milisegundos** hasta que la canceles.

## ¿Cómo programo una ejecución única con setTimeout?

`setTimeout` recibe una función anónima y un tiempo en milisegundos. El código no se imprime de inmediato, sino que espera a que el _event loop_ libere el turno :

javascript const timeout = setTimeout(() => { console.log("este mensaje aparece después de dos segundos"); }, 2000);

Si corres `node timers.js`, vas a ver primero la hora actual y luego, dos segundos después, el mensaje diferido.

## ¿Qué diferencia hay entre setImmediate y setTimeout?

`setImmediate` no recibe tiempo: ejecuta su callback en la **próxima iteración del bucle**, casi inmediatamente después de que termine la fase actual.

```javascript s
etImmediate(() => { console.log("este mensaje aparece en la próxima iteración del bucle"); });
```

En la práctica aparece justo después de los `console.log` síncronos y antes de cualquier `setTimeout` con delay mayor a cero.

## ¿Cómo creo un intervalo repetitivo con setInterval?

`setInterval` ejecuta el callback cada cierto tiempo de forma indefinida. Por eso casi siempre lo guardas en una constante para poder cancelarlo después :

javascript const intervalID = setInterval(() => { console.log("este mensaje aparece cada tres segundos"); }, 3000);

## ¿Cómo cancelo timers con clearTimeout y clearInterval?

La cancelación es donde el módulo brilla en escenarios reales. Imagina que disparas una notificación a un usuario, pero si el proceso falla antes, necesitas abortar ese envío. Para eso existen `clearTimeout` y `clearInterval`.

> **¿Cómo cancelo un setInterval?** Guarda la referencia que devuelve `setInterval` en una constante y pásala a `clearInterval(intervalID)` dentro de un `setTimeout` con el tiempo límite.

## ¿Cómo detengo un intervalo después de 10 segundos?

La estructura típica es anidar un `setTimeout` que llama a `clearInterval` cuando se cumple el tiempo deseado:

```javascript 
setTimeout(() => { clearInterval(intervalID); console.log("cancelar el intervalo después de 10 segundos"); }, 10000);
```

El intervalo dispara su mensaje cada 3 segundos, y al llegar a los 10 segundos se limpia y deja de imprimir.

## ¿Cómo evito que un setTimeout llegue a ejecutarse?

Mismo principio: guarda el ID y pásalo a `clearTimeout` antes de que se cumpla el delay :

```javascript 
const timeoutID = setTimeout(() => { console.log("este mensaje nunca aparecerá"); }, 10000);

clearTimeout(timeoutID);
```

Aunque programaste el mensaje para 10 segundos, lo limpias inmediatamente después de crearlo, así que nunca se imprime.

## ¿En qué orden se ejecutan los timers en Node.js?

Cuando corres el script completo, el orden de salida revela cómo Node.js prioriza las tareas. Primero se ejecutan los `console.log` síncronos como la _hora actual_ y la _hora final_, después entra `setImmediate` en la siguiente iteración, luego aparece el `setTimeout` de 2 segundos, y finalmente el `setInterval` empieza a disparar cada 3 segundos hasta que `clearInterval` lo apaga a los 10 segundos.

Este orden no es arbitrario: responde al _event loop_ de Node, que procesa fases distintas para timers, callbacks de I/O, immediates y close handlers.

## ¿Para qué sirven los timers en una aplicación real?

- Programar **notificaciones diferidas** que pueden cancelarse si el proceso falla.
- Ejecutar **tareas periódicas** como polling a una API o limpieza de cache.
- Diferir trabajo pesado a la **próxima iteración del bucle** con `setImmediate` para no bloquear el flujo actual.
- Implementar **timeouts de seguridad** que aborten operaciones que tardan demasiado.