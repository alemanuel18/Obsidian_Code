En Vue 3, las herramientas `reactive` y `ref` son fundamentales para trabajar con reactividad. Ambas tienen funciones clave pero diferentes, y entender sus diferencias te ayudará a elegir la más adecuada según tu caso de uso. En este artículo, explicaremos las diferencias entre `reactive` y `ref`, sus usos típicos, y ejemplos prácticos.

**¿Qué es `reactive`?**

`reactive` convierte un objeto en reactivo. Esto significa que Vue rastreará los cambios realizados en las propiedades del objeto y actualizará la interfaz de usuario de forma reactiva.

Uso típico

Usa `reactive` cuando trabajas con un **objeto** que tiene varias propiedades y necesitas que todas sean reactivas.

Ejemplo

```jsx
import { reactive } from 'vue';

const state = reactive({
  count: 0,
  message: 'Hola mundo'
});

// Reactividad
state.count++; // Vue rastrea este cambio
state.message = 'Adiós mundo'; // También reactivo
```

⚠️ Nota importante

Cuando desestructuras un objeto `reactive`, las propiedades individuales **pierden la reactividad**:

```jsx
const { count } = state; // No reactivo
```

En este caso, es mejor trabajar con el objeto completo.

**¿Qué es `ref`?**

`ref` crea un contenedor reactivo para un **valor único**. Este valor puede ser un número, una cadena, un booleano o incluso un objeto. Para acceder o modificar el valor, necesitas usar la propiedad `.value`.

Uso típico

Usa `ref` cuando trabajes con un **valor primitivo** o prefieras una sintaxis más explícita para manejar la reactividad.

Ejemplo

```jsx
import { ref } from 'vue';

const count = ref(0);

// Reactividad
count.value++; // Vue rastrea este cambio
```

Usando `ref` con objetos

Aunque puedes usar `ref` con objetos, recuerda que el acceso debe realizarse siempre a través de `.value`:

```jsx
const state = ref({ count: 0, message: 'Hola mundo' });
state.value.count++; // Reactivo
```

---

**Diferencias clave**

|Característica|`reactive`|`ref`|
|---|---|---|
|**Qué maneja**|Objetos con múltiples propiedades|Valores únicos o cualquier valor|
|**Acceso a datos**|Directo|A través de `.value`|
|**Soporte de desestructuración**|No conserva reactividad al desestructurar|Mantiene reactividad si se usa `.value`|
|**Uso principal**|Estados complejos (objetos y arrays)|Estados simples o valores únicos|

---

**¿Cuándo usar cada uno?**

Usa `reactive` cuando:

- Necesites manejar un estado complejo con múltiples propiedades y seguir seguimiento en niveles más profundos del objeto.
- Quieras una sintaxis más simple para acceder a las propiedades del objeto.

Ejemplo:

```jsx
const state = reactive({
  user: 'Enrique',
  age: 30
});
```

Usa `ref` cuando:

- Trabajes con un valor único (número, cadena, booleano, etc.).
- Prefieras controlar explícitamente el acceso mediante `.value`.

Ejemplo:

```jsx
const count = ref(0);
```

---

**Conclusión**

Ambas herramientas tienen su lugar en Vue 3. Mientras `reactive` es ideal para manejar objetos con varias propiedades, `ref` es perfecto para valores simples o cuando necesitas control explícito.

Comprender cómo funcionan te ayudará a escribir código más claro y eficiente en tus proyectos de Vue.