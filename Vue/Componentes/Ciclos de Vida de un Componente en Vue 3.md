En Vue 3, los ciclos de vida de un componente nos permiten ejecutar código en momentos específicos de su existencia, como cuando se crea, se monta en el DOM, se actualiza o se destruye.

Comprender estos ciclos es clave para manejar correctamente eventos, llamadas a API y optimizar el rendimiento de la aplicación.

## Etapas del Ciclo de Vida

Vue 3 ofrece varias etapas en el ciclo de vida de un componente, que se los principales se pueden dividir en:

**Fase de Creación**

- **`setup()`**: Se ejecuta antes de que el componente se monte. Es donde definimos el estado reactivo, efectos secundarios y funciones.

**Fase de Montaje**

- **`onBeforeMount()`**: Se ejecuta justo antes de que el componente se agregue al DOM.
- **`onMounted()`**: Se ejecuta después de que el componente ha sido montado en el DOM.

**Fase de Actualización**

- **`onBeforeUpdate()`**: Se ejecuta antes de actualizar el DOM cuando los datos reactivos cambian.
- **`onUpdated()`**: Se ejecuta justo después de que la actualización en el DOM ha finalizado.

**Fase de Desmontaje**

- **`onBeforeUnmount()`**: Se ejecuta justo antes de que el componente sea eliminado del DOM.
- **`onUnmounted()`**: Se ejecuta después de que el componente ha sido eliminado del DOM.

Para entender mejor estos ciclos, vamos a construir un contador simple que registre eventos en la consola según su ciclo de vida.

Para hacer uso del ciclo de vida de Vue nos apoyamos de unas funciones llamadas [lifecycle hooks](https://vuejs.org/guide/essentials/lifecycle).

```jsx
<script setup>
import { ref, onMounted, onBeforeUnmount, onUpdated } from 'vue';

const count = ref(0);

const increment = () => {
  count.value++;
};

onMounted(() => {
  console.log('Componente montado en el DOM');
});

onUpdated(() => {
  console.log(`El contador se ha actualizado a: ${count.value}`);
});

onBeforeUnmount(() => {
  console.log('Componente a punto de ser eliminado del DOM');
});
</script>

<template>
  <div>
    <h1>Contador: {{ count }}</h1>
    <button @click="increment">Incrementar</button>
  </div>
</template>
```

En este pequeño componente suceden multiples cambios aunque no nos demos cuenta incluso antes de que entre en pantalla. Esto lo podemos visualizar en los siguientes puntos:

- **Cuando el componente se monta (`onMounted`)**, se imprime un mensaje en la consola.
- **Cada vez que se actualiza (`onUpdated`)**, se registra el nuevo valor del contador.
- **Antes de que se elimine (`onBeforeUnmount`)**, se imprime un mensaje para indicar que el componente está por desmontarse.

## ¿Cuándo Usar los Hooks del Ciclo de Vida?

- **`onMounted()`**: Para inicializar datos o realizar llamadas a API.
- **`onUpdated()`**: Para ejecutar código después de un cambio reactivo.
- **`onBeforeUnmount()`**: Para limpiar eventos, timers o conexiones de WebSockets.

Con este conocimiento, puedes manejar de manera eficiente el estado y eventos en tus componentes Vue 3. Ojo, solo ten cuidado en cómo los usas porque podrías causar efectos secundarios que causen problemas de performance. Sigue explorando y experimentando con los ciclos de vida para optimizar tus aplicaciones.

¡Nos vemos en la siguiente clase!