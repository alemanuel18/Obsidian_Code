## ¿Qué son los EMITS en Vue?

¿Alguna vez te has preguntado cómo la comunicación entre componentes hijos y padres en Vue puede ser simplificada y eficaz? Aquí es donde entran en juego los EMITS. A través de los EMITS, Vue proporciona una manera de enviar eventos personalizados desde un componente hijo a uno padre. Es decir, puedes definir eventos propios de un componente que se activan bajo ciertas condiciones específicas. Aunque podrían implementarse como props, usar EMITS ofrece ventajas significativas al clarificar y estructurar mejor el código.

## ¿Cómo implementar un EMIT en Vue?

Imagina que tienes una barra de búsqueda que debe comunicar cambios al componente padre. Para lograr que funcione sin problemas, seguirás estos pasos:

1. **Define Props**: Primero, necesitas las propiedades. Por ejemplo, en un componente `game layout`, solicita los juegos a través de `defineProps`.
    
    ```javascript
    const props = defineProps({
	    games: {
		    type: Array,
		    required: true,
		},
	});
	``` 
    
2. **Referencia de Datos Originales**: Siempre es útil tener una copia original de los datos a manipular, especialmente para gestionar las mutaciones de una lista como juegos.
    
    ```javascript
    const gamesView = ref(state.games);
    ```
    
3. **EMIT personalizado**: Declara un EMIT, como `setGameView`, que permitirá modificar desde el componente padre.
    
    ```javascript
    const emit = defineEmits(['setGameView']);
    ```
    
4. **Usa el EMIT en la acción correspondiente**: Cuando la acción se dispara (por ejemplo, una búsqueda), usa el EMIT para enviar datos al componente padre.
    
    ```javascript
    emit('setGameView', filteredGames);
    ```
    

## ¿Cómo mejorar la funcionalidad de la barra de búsqueda?

El objetivo es lograr que tu barra de búsqueda interactúe perfectamente con la lista de `games`, ajustando el comportamiento según la entrada del usuario.

1. **Función de Búsqueda**: Implementa una función que filtre los `games` basado en una entrada.
    
    ```javascript
    const search = (input) => {
	    const termSearch = input.toLowerCase();
	    return props.games.filter(game =>
	    game.title.toLowerCase().includes(termSearch)
	    );
    };
    ```
    
2. **Manejo de Resultados**: Asegúrate que si la búsqueda es vacía, la lista se restablezca a su estado inicial.
    
    ```javascript
    if (termSearch === '') {
	    emit('setGameView', props.games);
	return;
	}
	```
    

### Solucionando errores comunes

Implementando características como filtros y eventos, pueden surgir varios inconvenientes. Aquí algunos consejos para gestionar estos desafíos:

- **Chequea las Reglas de Mutación**: Las props no deben ser mutadas directamente ya que Vue prohibe esto en aras de mantener la unidireccionalidad de los datos.
    
- **Casting de Variables**: Asegúrate de que las variables sean interpretadas correctamente, ya que un tipo incorrecto puede resultar en errores de tipo no manejados.
    

### Retos y mejoras sugeridas

La implementación de un EMIT básico es solo el comienzo. Aquí algunas ideas para refinar y extender tu proyecto:

1. **Implementar Observadores (Watchers)**: Para automatizar el restablecimiento de la vista completa de `games`, podrías usar un watcher que escuche cambios en el input de búsqueda.
    
2. **Añadir un Botón de Reseteo**: Considera incluir un botón que solo aparezca cuando se haya realizado una búsqueda, permitiendo al usuario restablecer la lista a su estado original con un clic.
    
3. **Simplificación Algorítmica**: Mejorar el algoritmo de búsqueda para buscar de manera más eficiente y sin problemas de lógica.
    

Experimenta y personaliza estos elementos; la práctica te acercará a soluciones más óptimas y robustas. Tu aplicación será cada vez más dinámica, lo que hará que tanto tú como los usuarios tengan una experiencia enriquecedora. Si te encuentras con dudas durante este proceso, recuerda que el conocimiento se profundiza cuando se enfrenta con retos y errores.