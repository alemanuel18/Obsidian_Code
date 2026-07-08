## ¿Qué son los Watchers en Vue y cómo utilizarlos?

Los **Watchers** en Vue son una poderosa herramienta que permite a los desarrolladores observar y reaccionar ante cambios en el estado de una aplicación. Son muy útiles cuando se quiere ejecutar una acción cada vez que una propiedad reactiva cambie de valor. En esta clase aprenderemos a utilizar los Watchers para monitorear el estado de nuestro componente 'game counter' y disparar efectos visuales con la librería JS confetti cuando el usuario acierte un número.

## ¿Cómo preparar el entorno para trabajar con Watchers?

La preparación del entorno es fundamental antes de empezar a usar Watchers. Primero, asegúrate de estar en la rama de trabajo apropiada, en este caso, la rama `vue-watcher-start`, que contiene pequeños ajustes en la lógica del contador. Estos ajustes incluyen:

- Un generador de números aleatorios para la inicialización del contador.
- Lógica que evita que el contador supere el valor máximo o se torne negativo.

Para esto, utiliza el comando en terminal:

```bash
git checkout vue-watcher-start
```

## ¿Cuál es el objetivo del juego con el contador?

El juego consiste en presionar botones para incrementar o decrementar un contador hasta acertar un número generado aleatoriamente, el cual se debe adivinar. Cuando el usuario acierta, el objetivo es lanzar confetti como señal de triunfo.

## ¿Cómo implementar JS confetti en el juego?

Para empezar, debemos instalar la librería JS confetti. Primero, carga la dependencia con:

```bash
npm install js-confetti
```

Lo que buscamos es que al acertar el número, se dispare el confetti. En lugar de poner lógica de verificación dentro de las funciones de incremento o decremento, utilizaremos un Watcher para monitorear el estado del contador:

## ¿Cómo utilizar WatchEffect para monitorear cambios?

El `WatchEffect` permite ejecutar un efecto cada vez que un estado reacivo cambie dentro del cuerpo de la función:

```javascript
watchEffect(() => {
  console.log(`El contador ha cambiado a: ${counter.value}`);
});
```

## ¿Por qué elegir 'watch' en lugar de 'watchEffect'?

Aunque `WatchEffect` es útil, suele ser más controlado usar `watch`, dado que permite especificar exactamente qué propiedades reactivas queremos monitorear, evitando ejecuciones innecesarias en múltiples cambios de estados:

```javascript
watch(counter, (newValue) => {
  console.log(`El contador ha cambiado a: ${newValue}`);
  if (newValue === numberToGuess) {
    jsConfettiInstance.addConfetti();
  }
});
```

Este método mejora la eficiencia y performance al limitar las propiedades observadas.

## ¿Cómo limitar los efectos múltiples de confetti?

Para evitar que el confetti se dispare múltiples veces, introduce un estado adicional que marque si el usuario ya ha ganado:

```javascript
const win = ref(false);

watch(counter, (newValue) => {
  if (newValue === numberToGuess && !win.value) {
    jsConfettiInstance.addConfetti();
    win.value = true;
  }
});
```

Este estado se actualizará a `true` cuando se acierte, desactivando los botones para evitar nuevas modificaciones.

## ¿Qué consejos se deben seguir al usar Watchers?

- Usa `watch` sobre `watchEffect` para un control más preciso.
- Limita la cantidad de propiedades observadas para evitar problemas de rendimiento.
- Implementa lógica con precaución para no causar múltiples renderizados innecesarios.

Los Watchers son una funcionalidad clave de Vue cuando se desea realizar acciones específicas ante cambios de estado, pero su uso indebido puede afectar la performance de la aplicación. Siempre es recomendable aplicar prácticas óptimas para un desarrollo fluido y eficiente.