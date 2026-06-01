# Fundamentos de CSS

**CSS** (Hojas de Estilo en Cascada, por sus siglas en inglés) es el lenguaje utilizado para describir la presentación, el diseño y el formato de los documentos estructurados en HTML. Mientras HTML define el significado, CSS describe cómo debe ser renderizado ese contenido en las pantallas.

A continuación, exploraremos los conceptos y propiedades fundamentales de CSS, su funcionamiento, valores y ejemplos prácticos:

### 1. Selectores, Especificidad y Combinadores
Los selectores son herramientas que te permiten "apuntar" a los elementos HTML exactos a los que deseas aplicarles un estilo. 
*   **Selectores básicos**: Puedes seleccionar por etiqueta (ej. `p`), por clase (`.clase`) o por ID (`#id`).
*   **Especificidad**: Es el sistema que usa CSS para decidir qué regla gana cuando hay un conflicto. Un ID tiene mayor peso (prioridad) que una clase, y una clase tiene mayor peso que una etiqueta. Si usas la declaración `!important`, esta sobreescribirá cualquier otra regla.
*   **Combinadores**: Definen la relación entre selectores.
    *   **Descendiente (espacio)**: Selecciona todos los elementos dentro de un ancestro (ej. `div p`).
    *   **Hijo directo (`>`)**: Selecciona solo a los hijos directos (ej. `div > p`).
    *   **Hermano adyacente (`+`)**: Selecciona el elemento que está inmediatamente después (ej. `h1 + p`).

**Ejemplo de uso:**
```css
/* Selector de etiqueta */
p {
  color: black; /* Propiedad heredable */
}

/* Selector de clase con mayor especificidad */
.texto-destacado {
  color: blue;
}

/* Selector de ID (la máxima especificidad) */
#titulo-principal {
  color: red;
}

/* Combinador de hijo directo */
article > p {
  font-weight: bold;
}
```

### 2. Pseudo-clases y Pseudo-elementos
Permiten aplicar estilos basados en estados dinámicos del elemento o añadir elementos que no existen en el HTML original.
*   **Pseudo-clases (`:`)**: Representan el estado o las emociones del elemento. 
    *   *Valores comunes*: `:hover` (cuando el cursor pasa por encima), `:active` (cuando se hace clic), `:first-child` (selecciona el primer hijo, excelente para no ensuciar el HTML con clases extra).
*   **Pseudo-elementos (`::`)**: Actúan como "accesorios" que enriquecen el contenido sin modificar el HTML.
    *   *Valores comunes*: `::before` (inserta contenido antes), `::after` (inserta contenido después), `::first-letter` (para hacer letras capitales).

**Ejemplo de uso:**
```css
/* Pseudo-clase: Cambia de color al pasar el mouse */
button:hover {
  background-color: #2ecc71;
}

/* Pseudo-elemento: Añade unas comillas automáticamente antes de una cita */
blockquote::before {
  content: '"';
  font-size: 2rem;
  color: gray;
}
```

### 3. El Modelo de Caja (Box Model)
En CSS, **absolutamente todos los elementos se comportan como cajas rectangulares**. Este modelo define cómo se distribuye el tamaño de un elemento y el espacio a su alrededor.
*   **`content`**: Es el contenido real del elemento (texto, imágenes) al que se le aplican `width` (ancho) y `height` (alto).
*   **`padding`**: Es el margen interno. Es la distancia desde el contenido hasta el borde de la caja.
*   **`border`**: Es la línea que rodea al padding y al contenido.
*   **`margin`**: Es el espacio externo. Empuja a los demás elementos para separarlos de la caja.
*   **`box-sizing`**: Es una propiedad vital. Su valor `border-box` hace que el `padding` y el `border` se calculen hacia adentro, evitando que la caja crezca y rompa tu diseño.

**Ejemplo de uso:**
```css
/* Recomendación global para evitar que las cajas se deformen */
* {
  box-sizing: border-box; 
}

.tarjeta {
  width: 300px;
  padding: 20px; /* Espacio interno */
  border: 2px solid #ccc; /* Borde visible */
  margin: 15px; /* Separación con otras tarjetas */
}
```

### 4. Posicionamiento (Position y Z-Index)
La propiedad `position` controla con precisión la ubicación de un elemento respecto a la pantalla o a su contenedor.
*   **`position`**: 
    *   *Valores*: `static` (por defecto, sigue el flujo normal), `relative` (se mueve desde su posición original sin alterar a sus hermanos), `absolute` (vuela libremente respecto a su ancestro relativo más cercano), `fixed` (se queda fijo en la pantalla, ideal para menús), `sticky` (actúa como relativo hasta que se hace scroll y luego se queda fijo).
*   **`z-index`**: Maneja el apilamiento en 3D (eje Z). Permite que un elemento se sobreponga a otro mediante valores numéricos (ej. `z-index: 10;`).
*   **`overflow`**: Decide qué pasa si el contenido es más grande que su caja. Valores: `visible` (por defecto), `hidden` (recorta y oculta el sobrante), `scroll` o `auto` (agrega barras de desplazamiento).

**Ejemplo de uso:**
```css
.contenedor-padre {
  position: relative; /* Se convierte en el punto de referencia */
}

.etiqueta-hija {
  position: absolute; /* Se mueve libremente respecto al padre */
  top: 10px;
  right: -5px;
  z-index: 2; /* Se asegura de estar por encima del contenido del padre */
}
```

### 5. Unidades de Medida y Variables CSS
El uso de medidas y variables correctas es la diferencia entre un código difícil de mantener y uno profesional.
*   **Unidades de Medida**:
    *   **`px`** (píxeles): Medida absoluta, estática.
    *   **`rem`**: Medida relativa al tamaño de fuente de la raíz (`html`). Es la medida estándar recomendada para tipografías y contenedores, ya que mejora radicalmente la accesibilidad si el usuario hace la letra de su navegador más grande.
    *   **`em`**: Relativo al tamaño de fuente de su elemento padre (se usa en componentes modulares, como botones).
*   **Variables CSS (`--`)**: Son "cajas" para guardar valores como colores primarios o tipografías, permitiendo mantener la consistencia en el sitio y cambiar todo modificando una sola línea. Se declaran en `:root` y se invocan con `var()`.

**Ejemplo de uso:**
```css
/* Declaración de variables globales */
:root {
  --color-primario: #3498db;
  --color-peligro: #e74c3c;
  --fuente-base: 1.6rem; /* Equivale a 16px normalmente */
}

.boton {
  background-color: var(--color-primario);
  font-size: var(--fuente-base);
  padding: 1em 2em; /* Crece en proporción al tamaño de su fuente */
}

.boton--error {
  background-color: var(--color-peligro);
}
```

***

Para continuar con nuestra guía integral, dime con cuál de estos temas avanzados te gustaría seguir:
1. **Layouts Modernos (Flexbox y Grid)**
2. **Propiedades Tipográficas, Sombras y Degradados**
3. **Efectos, Transiciones y Animaciones**
4. **Responsive Design y Mobile First**