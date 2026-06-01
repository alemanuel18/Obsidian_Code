# Accesibilidad Web y SEO

La **Accesibilidad Web** y el **SEO** (Optimización para Motores de Búsqueda) son dos conceptos que trabajan de la mano. Escribir un código accesible no solo garantiza que las personas con discapacidades visuales o motoras puedan navegar por tu sitio utilizando lectores de pantalla, sino que también ayuda enormemente a que Google y otros navegadores **entiendan el propósito y la estructura de tu contenido**.

A continuación, desarrollamos las etiquetas HTML y propiedades CSS esenciales para cumplir con estos estándares.

## 1. HTML: Semántica, Meta tags y Atributos ARIA

En HTML, la forma en la que etiquetas la información le dice directamente a los motores de búsqueda de qué trata tu página y le da contexto a las tecnologías de asistencia.

### Etiquetas y atributos involucrados:

*   **`<meta>`**: Se colocan siempre dentro del `<head>` y no son visibles para el usuario, pero son vitales para los navegadores y buscadores. Las más importantes son:
    *   `name="viewport"`: Esencial para el posicionamiento y la experiencia en móviles, hace que el diseño sea responsivo.
    *   `name="description"`: Define el resumen que Google muestra en los resultados de búsqueda. 
    *   `name="robots"`: Le indica a los motores de búsqueda qué pueden indexar y rastrear de tu sitio.
    *   **Open Graph (`property="og:..."`)**: Meta tags específicas para optimizar cómo se previsualiza tu contenido cuando alguien lo comparte en redes sociales.
*   **Estructura Semántica Avanzada**:
    *   **`<article>`**: Representa contenido que tiene sentido y valor por sí mismo, y que podría ser distribuido de forma completamente independiente (como un artículo de un blog o una noticia).
    *   **`<section>`**: A diferencia de *article*, se utiliza de forma más general para agrupar contenido que está temáticamente relacionado dentro de un documento.
*   **Atributo `alt` en `<img>`**: Es una **obligación y prioridad** para la accesibilidad. Proveer un texto alternativo describe la imagen para quienes usan lectores de pantalla y le da contexto a los motores de búsqueda.
*   **Atributos ARIA (Accessible Rich Internet Applications)**: Son atributos especiales (como `aria-label`, `aria-hidden`, o `role`) que complementan al HTML cuando las etiquetas nativas no son suficientes. Son la base para que los lectores de pantalla puedan interpretar menús desplegables, modales o notificaciones dinámicas.

### Ejemplo de uso en HTML:
```html
<!DOCTYPE html>
<html lang="es"> <!-- Definir el idioma es vital para el SEO y lectores de pantalla -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- Etiquetas SEO escenciales -->
  <title>Guía de Accesibilidad y SEO</title>
  <meta name="description" content="Aprende a estructurar tus páginas web para que sean accesibles y posicionen en Google.">
  <meta name="robots" content="index, follow">
  
  <!-- Open Graph para Redes Sociales -->
  <meta property="og:title" content="Guía de Accesibilidad y SEO">
  <meta property="og:description" content="Optimiza tu web para todos los usuarios.">
</head>
<body>
  <main>
    <section>
      <!-- Usamos article porque es un contenido independiente -->
      <article>
        <h1>Mejorando el SEO</h1>
        <p>Una buena imagen siempre debe llevar su atributo alt.</p>
        <!-- El atributo alt es vital para SEO y lectores de pantalla -->
        <img src="grafico-seo.jpg" alt="Gráfico de barras mostrando el crecimiento del SEO">
      </article>
    </section>

    <!-- Botón con atributo ARIA para mejorar la accesibilidad -->
    <button aria-label="Cerrar el menú principal" onclick="cerrarMenu()">X</button>
  </main>
</body>
</html>
```

---

## 2. CSS: Propiedades para Mejorar la Accesibilidad (UX)

El CSS no mejora el SEO de forma directa, pero sí impacta las *Core Web Vitals* de Google (métricas de experiencia de usuario) y la navegabilidad, las cuales **sí afectan el posicionamiento**. Un sitio con mala legibilidad o donde el usuario no se puede mover usando el teclado, será penalizado.

### Propiedades relacionadas y valores:

*   **`outline`**: Delinea un elemento para resaltar que está enfocado. A diferencia de `border`, el `outline` no altera el modelo de caja (no empuja a los otros elementos ni cambia el tamaño del componente). Es crucial para los usuarios que navegan usando la tecla `Tab`.
    *   *Valores*: Grosor, estilo y color (ej. `2px solid blue`).
*   **Pseudo-clase `:focus` y `:focus-visible`**: Aplican los estilos exactamente cuando un elemento interactivo (como un enlace, botón o input de formulario) recibe el foco mediante el teclado o el clic.
*   **Contraste de `color` y `background-color`**: Aunque parezca básico, asegurar que el color del texto destaque claramente contra el color de fondo es la regla de oro de la accesibilidad. Herramientas externas o extensiones verifican que el contraste cumpla con el estándar WCAG (Web Content Accessibility Guidelines).
*   **Clase oculta solo para lectores de pantalla (Screen-reader only)**: *Nota: Esta es una técnica estándar de la industria, muy popular en la comunidad, que utiliza múltiples atributos CSS para ocultar un elemento visualmente pero dejarlo disponible para el lector de voz.* Nunca se debe usar `display: none` para esto, porque los lectores de voz también lo ignorarían.

### Ejemplo de uso en CSS:
```css
/* --- NAVEGACIÓN ACCESIBLE POR TECLADO --- */

/* Todos los enlaces y botones interactivos */
a, button {
  padding: 10px 15px;
  background-color: #3498db;
  color: #ffffff; /* Alto contraste para buena legibilidad */
  border: none;
  cursor: pointer;
}

/* Cuando el usuario usa el teclado (Tab) para navegar */
a:focus, button:focus {
  /* Resalta claramente qué elemento está seleccionado */
  outline: 3px solid #f1c40f; 
  outline-offset: 4px; /* Separa el delineado del borde del elemento */
}

/* --- CLASE DE UTILIDAD: SOLO LECTOR DE PANTALLA (sr-only) --- */
/* Se aplica a textos que sirven para dar contexto auditivo pero rompen el diseño visual */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0); /* Recorta visualmente el elemento por completo */
  border: 0;
}
```

¿Qué tema te gustaría que exploráramos ahora? Podemos adentrarnos de lleno en **Layouts Modernos (Grid y Flexbox)**, **Modelo de Caja (Box Model)** o pasar al mundo de las **Animaciones y Transiciones**.