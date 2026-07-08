## ¿Qué es un Composable y cómo puede ayudarme?

Los Composables son fragmentos de código reutilizables que te permiten aislar lógica compartida en tus proyectos Vue, siguiendo la práctica de "don't repeat yourself" (DRY). A medida que desarrollas una aplicación web que crece con el tiempo, es común encontrar lógica repetida en múltiples componentes. Los Composables te permiten encapsular esta lógica de manera que puedas utilizarla en varios lugares de tu aplicación sin tener que copiar y pegar el mismo código continuamente.

## ¿Cómo crear un Composable en Vue?

Para crear un Composable, debes seguir algunos pasos clave:

1. **Crea una carpeta para Composables:** Dentro de tu carpeta `src`, crea una subcarpeta llamada `Composables`. Aquí es donde almacenarás tus Composables.
    
2. **Crea el Composable:** Dentro de esta carpeta, crea un archivo con el nombre de tu Composable. Por ejemplo, para una función de obtención de datos, podrías llamar al archivo `useFetch.js`.
    
3. **Define la función del Composable:** En el archivo del Composable, exporta una función que recibirá los parámetros necesarios. Por ejemplo:
    
    ```javascript
	export function useFetch(apiUrl, onSuccess = () => {}) {
		const state = /* lógica para manejar el estado */;
		// Lógica para la petición a la API
		onSuccess(responseJson);
	    return { state };
	}
	```
    
4. **Aisla y generaliza la lógica de tu componente:** Mueve la lógica compartida de tu componente original al Composable. Por ejemplo, si tienes una función para obtener datos de una API, trasládala al Composable.
    
5. **Importa y usa el Composable en tus componentes:** Cuando necesites usar esta lógica en un componente, importa el Composable y úsalo según sea necesario.
    

## ¿Cómo asegurar que el Composable se use correctamente?

Al importar y usar un Composable, es importante considerar:

- **Manejo del estado:** Cuando declares un estado dentro de un Composable, asegúrate de retornarlo para que pueda ser utilizado en el componente importador.
    
- **Parámetros adecuados:** Asegúrate de pasar todos los parámetros necesarios al Composable. En el caso de `useFetch`, esto incluye la URL de la API y la función de callback.
    
- **Manejo de ciclos de vida:** Cuando trabajes con ciclos de vida dentro de Composables, como el uso de `onMounted`, ten cuidado de no causar efectos secundarios indeseados o renders múltiples innecesarios al manipular el estado.
    

## ¿Cómo manejar los estados de carga y errores?

El manejo de estados de carga y errores es fundamental para ofrecer una buena experiencia de usuario. Puedes integrar indicadores de carga y mensajes de error de manera eficiente utilizando directivas y componentes predefinidos, como el `SharedLoader` mencionado en el ejemplo:

- **Indicador de carga:** Importa un componente de carga y úsalo junto con una variable (`state.isLoading`) para mostrar el indicador mientras esperas la respuesta de la API.
    
    ```vue
    <template>
	    <SharedLoader v-if="state.isLoading" />
	    <GamesLayout v-else />
	</template>
	```
    

### Precauciones al usar Composables

Es importante no abusar de los Composables, especialmente al incluir ciclos de vida de Vue, pues podrían generar estados no deseados y múltiples redibujados. Usa Composables para aislar lógica común, pero siempre evalúa su impacto en el rendimiento y la claridad del código.

Por último, te animo a experimentar con Composables en tu aplicación. Intenta identificar lógica repetitiva que puedas encapsular, y observa cómo se simplifica y organiza tu código.