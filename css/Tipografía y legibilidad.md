# Tipografía y legibilidad

La tipografía no consiste únicamente en elegir una fuente atractiva, sino en garantizar que el contenido textual sea legible y la lectura cómoda para los usuarios. CSS ofrece múltiples propiedades de control de texto que impactan directamente en la experiencia de usuario y la accesibilidad.

A continuación, exploramos las propiedades tipográficas, su funcionamiento y buenas prácticas:

## 1. Fuentes Web (Web Fonts)
Para utilizar fuentes personalizadas (como las que ofrece Google Fonts) en lugar de las predeterminadas por el sistema operativo, estas deben integrarse en el documento HTML antes de ser llamadas en CSS.
*   **Implementación (`<link>`)**: Se enlaza dentro de la etiqueta `<head>` de HTML. Es una gran práctica incluir el atributo `rel="preconnect"` en enlaces previos al de la fuente; esto le indica al navegador que anticipe la conexión al servidor de Google, mejorando la optimización y velocidad de carga.
*   **Fuentes de respaldo (Fallbacks)**: Al declarar una fuente en CSS, siempre debes incluir como segunda opción una familia tipográfica genérica (como `sans-serif` o `serif`). Así, en caso de que tu fuente web falle al cargar, el navegador usará esa alternativa para no dejar el texto sin estilo.

## 2. Propiedades Tipográficas (`font-*`)
Se encargan de alterar el estilo, grosor y tamaño directo de los caracteres.
*   **`font-family`**: Define la fuente del elemento (ej. Arial, Helvetica, sans-serif).
*   **`font-size`**: Define el tamaño de la tipografía. 
    *   *Mejor práctica de accesibilidad*: Se recomienda **evitar el uso de `px`** (píxeles) estáticos, ya que impiden que el texto crezca si el usuario amplía la fuente predeterminada desde la configuración de su navegador (algo vital para personas con discapacidad visual). 
    *   En su lugar, **utiliza `rem`** (relativo al tamaño raíz de la página) para la estructura tipográfica principal, o **`em`** cuando desees que ciertos elementos (como un botón y su relleno) escalen en proporción a su texto interno.
*   **`font-weight`**: Define el grosor visual de la letra, desde `normal` hasta `bold` (negrita), o mediante escalas numéricas (ej. `400` para normal, `700` para negrita).
*   **`font-style`**: Se utiliza principalmente para transformar la tipografía a cursiva (`italic`).

## 3. Control de Texto (`text-*` y espaciados)
Estas propiedades se centran en el formato del bloque de texto, el flujo de lectura y sus decoraciones.
*   **`color`**: Determina el color del texto. Para que la legibilidad sea exitosa, es fundamental respetar un buen contraste entre el color del texto y el fondo.
*   **`line-height`**: Define el interlineado o espaciado vertical entre las líneas de un párrafo. Un valor óptimo de interlineado (como `1.5` o `1.6`) hace que un párrafo extenso no luzca amontonado y sea fácil de leer.
*   **`letter-spacing`**: Modifica la separación horizontal entre cada carácter, ideal para títulos impactantes.
*   **`text-align`**: Alinea el contenido del texto a nivel de bloque. Los valores comunes son `left` (izquierda), `center` (centro), `right` (derecha) o `justify` (justificado).
*   **`text-indent`**: Genera un sangrado (espaciado en blanco) únicamente en la primera línea de un bloque de texto, muy usado en redacciones clásicas o editoriales.
*   **`text-decoration`**: Añade líneas decorativas al texto. Se utiliza habitualmente con el valor `none` para eliminar el subrayado que los navegadores aplican por defecto a los enlaces, o `line-through` para tachados.
*   **`text-shadow`**: Crea sombras directamente en el texto. Puede utilizarse sutilmente para guiar la mirada y mejorar el contraste del título contra un fondo complejo.

---

## Ejemplo de uso (HTML y CSS)

```html
<!-- HTML -->
<head>
  <!-- Optimizando la conexión con preconnect -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <!-- Importando la fuente web 'Inter' -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" rel="stylesheet">
</head>
<body>
  <article class="articulo">
    <h1 class="articulo__titulo">La Legibilidad en la Web</h1>
    <p class="articulo__texto">
      Aprender a controlar la tipografía no solo hace que una página se vea profesional, sino que facilita enormemente la vida del usuario al consumir el contenido.
    </p>
  </article>
</body>
```

```css
/* CSS */

:root {
  /* Guardando la fuente web y su fallback genérico en una variable */
  --fuente-principal: 'Inter', sans-serif;
}

.articulo {
  font-family: var(--fuente-principal);
  color: #333333; /* Color oscuro para alto contraste sin ser negro puro */
  max-width: 600px;
}

.articulo__titulo {
  font-size: 2.5rem; /* Tamaño relativo y accesible (aprox 40px) */
  font-weight: 700; /* Grosor en negrita */
  text-align: center; /* Título centrado */
  letter-spacing: 2px; /* Mayor separación entre letras para dar estilo */
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1); /* Sombra sutil que aporta profundidad */
}

.articulo__texto {
  font-size: 1.125rem; /* Tamaño relativo y accesible (aprox 18px) */
  font-weight: 400; /* Grosor normal */
  line-height: 1.6; /* Interlineado amplio para una lectura cómoda */
  text-indent: 2rem; /* Sangría al inicio del párrafo */
  text-align: left; /* Alineación del bloque a la izquierda */
}
```
