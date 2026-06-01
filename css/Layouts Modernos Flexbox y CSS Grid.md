# Layouts Modernos (Flexbox y CSS Grid)

En el desarrollo web actual, las técnicas tradicionales para estructurar una página (como el uso de tablas o la propiedad `float`) han sido reemplazadas por herramientas de diseño mucho más robustas y nativas: **Flexbox** y **CSS Grid Layout**. 

Aunque ambos se aplican mediante CSS a contenedores HTML (como `<div>`, `<main>`, `<header>`, `<nav>`, etc.), cada uno tiene un propósito específico: **Grid se utiliza generalmente para el diseño estructural o general de la página (el esqueleto), mientras que Flexbox es ideal para alinear el contenido interno de esos contenedores**.

A continuación, exploraremos ambos modelos:

---

## 1. Flexbox (Flexible Box Layout)

Flexbox es un sistema de diseño **unidimensional**, lo que significa que maneja el diseño en una sola dirección a la vez: en una fila o en una columna. Actúa como un **"organizador automático de cajas"**, donde los elementos hijos se alinean y distribuyen de manera flexible según el espacio disponible en su contenedor.

### Propiedades clave en el Contenedor Padre:
*   **`display: flex;`**: Activa el modelo Flexbox en el contenedor.
*   **`flex-direction`**: Define el eje principal. Valores: `row` (fila, por defecto), `column` (columna), `row-reverse`, `column-reverse`.
*   **`justify-content`**: Alinea los elementos a lo largo del eje principal. Valores: `flex-start`, `center`, `flex-end`, `space-between` (separa los elementos a los extremos), `space-around`, `space-evenly`.
*   **`align-items`**: Alinea los elementos a lo largo del eje transversal (perpendicular al principal). Valores: `stretch` (por defecto, los estira), `center`, `flex-start`, `flex-end`.
*   **`flex-wrap`**: Define si los elementos deben saltar a la siguiente línea si no caben. Valores: `nowrap` (por defecto), `wrap`, `wrap-reverse`.

### Propiedades clave en los Elementos Hijos (Items):
*   **`flex-grow`**: Define la capacidad de un elemento para crecer y ocupar el espacio libre restante. Un valor de `1` hace que ocupe todo el espacio posible; si varios tienen `1`, se reparten el espacio en partes iguales. Puede recibir valores decimales o enteros mayores a cero.
*   **`flex-shrink`**: Define la capacidad del elemento para encogerse si falta espacio.
*   **`align-self`**: Permite sobrescribir la alineación dictada por `align-items` para un elemento individual.

**Ejemplo de uso (Flexbox en una barra de navegación):**
```html
<nav class="menu">
  <div class="menu__logo">MiMarca</div>
  <ul class="menu__enlaces">
    <li><a href="#">Inicio</a></li>
    <li><a href="#">Servicios</a></li>
    <li><a href="#">Contacto</a></li>
  </ul>
</nav>
```
```css
.menu {
  display: flex;
  flex-direction: row; /* Elementos en fila */
  justify-content: space-between; /* El logo a la izquierda, enlaces a la derecha */
  align-items: center; /* Centrados verticalmente */
  background-color: #2c3e50;
  padding: 1rem 2rem;
  color: white;
}

.menu__enlaces {
  display: flex;
  gap: 1.5rem; /* Separación moderna entre los flex-items */
  list-style: none; /* Quitamos las viñetas */
  margin: 0;
  padding: 0;
}
```

---

## 2. CSS Grid Layout

CSS Grid es un sistema de diseño **bidimensional** que organiza el contenido simultáneamente en **filas y columnas**. Es la herramienta más poderosa para crear la estructura o "plano" principal de una página (por ejemplo, definir dónde va el *header*, la barra lateral, el contenido principal y el *footer*).

### Conceptos Clave de Grid:
*   **Grid Container**: El elemento padre que contiene la cuadrícula.
*   **Grid Lines (Líneas)**: Las líneas divisorias horizontales y verticales que forman la cuadrícula.
*   **Grid Cell (Celda)**: El espacio unitario mínimo delimitado por 4 líneas.
*   **Grid Area (Área)**: Un espacio rectangular que abarca varias celdas (filas y columnas). Permite "nombrar zonas" para organizar el contenido fácilmente, como si armaras un rompecabezas.

### Propiedades clave en el Contenedor Padre:
*   **`display: grid;`**: Activa la grilla.
*   **`grid-template-columns`** y **`grid-template-rows`**: Definen cuántas columnas/filas habrá y qué tamaño tendrán. Puedes usar medidas como `px`, `%`, o la unidad fraccional especial de Grid: **`fr`** (fracción del espacio disponible). Funciones como `repeat()` facilitan la declaración de columnas múltiples.
*   **`grid-template-areas`**: Permite asignar nombres a las áreas de la grilla para "dibujar" la estructura en código.
*   **`gap`**: Define el espaciado (canaleta) exactamente igual entre las filas y las columnas (anteriormente conocido específicamente como `grid-gap`, pero `gap` es la sintaxis moderna recomendada que sirve tanto para Flexbox como para Grid).

### Propiedades clave en los Elementos Hijos:
*   **`grid-area`**: Asigna el elemento a un área con nombre definida en el padre.
*   **`grid-column`** y **`grid-row`**: Permiten indicar desde qué línea hasta qué línea debe extenderse un elemento (ej. `grid-column: 1 / 3;` para ocupar dos columnas).

**Ejemplo de uso (Grid para una estructura de página completa):**
```html
<div class="layout-principal">
  <header class="cabecera">Cabecera</header>
  <aside class="barra-lateral">Menú Lateral</aside>
  <main class="contenido">Contenido Principal</main>
  <footer class="pie-pagina">Pie de Página</footer>
</div>
```

```css
.layout-principal {
  display: grid;
  /* Definimos 2 columnas: la 1ra de 250px fija, la 2da ocupa el resto (1fr) */
  grid-template-columns: 250px 1fr;
  /* Definimos 3 filas: header y footer automáticos, contenido estirado (1fr) */
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
  gap: 1rem; /* Espaciado entre todas las áreas */

  /* Dibujamos la estructura visualmente */
  grid-template-areas: 
    "header header"
    "sidebar main"
    "footer footer";
}

/* Asignamos cada etiqueta a su área correspondiente */
.cabecera { 
  grid-area: header; 
  background-color: #e74c3c;
}
.barra-lateral { 
  grid-area: sidebar; 
  background-color: #f1c40f;
}
.contenido { 
  grid-area: main; 
  background-color: #ecf0f1;
}
.pie-pagina { 
  grid-area: footer; 
  background-color: #34495e;
}
```
