# Contenido Multimedia

La integración de contenido multimedia (imágenes, audios y videos) es esencial para el desarrollo web moderno. Para lograrlo correctamente, es indispensable aplicar técnicas de optimización y responsividad que mejoren el rendimiento y la accesibilidad.

## 1. HTML: Etiquetas de Contenido Multimedia

En HTML5 existen múltiples etiquetas diseñadas específicamente para manejar la carga de archivos multimedia de forma nativa e inteligente.

### Etiquetas involucradas y funcionamiento:

*   **`<img>`**: Etiqueta de autocierre utilizada para incrustar imágenes.
    *   **Atributos clave**: `src` (ruta del archivo) y `alt` (texto alternativo obligatorio para accesibilidad). 
    *   **Atributos de rendimiento**: **`loading="lazy"`** le dice al navegador que no cargue la imagen hasta que el usuario haga scroll hacia ella, mientras que **`decoding="async"`** permite que la imagen se decodifique en segundo plano sin bloquear el renderizado de la página completa.
    *   **Atributos responsivos (`srcset` y `sizes`)**: Permiten que el navegador elija la resolución de imagen más óptima según el tamaño de la pantalla, ideal para ahorrar datos.
*   **`<picture>` y `<source>`**: Actúan como un contenedor avanzado. Se utiliza específicamente para la **"dirección de arte"**, permitiendo forzar cambios visuales drásticos según el dispositivo (por ejemplo, mostrar una imagen cuadrada en móviles y una panorámica en escritorio).
*   **`<video>` y `<audio>`**: Permiten reproducir contenido multimedia directamente en el navegador sin software externo.
    *   **Atributos clave**: **`poster`** muestra una imagen de portada antes de reproducir el video. **`preload="none"`** es vital para evitar el consumo innecesario del ancho de banda y datos de los usuarios, indicándole al navegador que no descargue el video hasta que el usuario presione play.
*   **`<iframe>`**: Se utiliza frecuentemente para incrustar reproductores externos de video como los de YouTube o Vimeo.
*   **`<figure>` y `<figcaption>`**: Agrupan semánticamente una imagen o video junto a su título o descripción visible.

**Ejemplo de uso (HTML):**
```html
<!-- Imagen con carga optimizada y perezosa -->
<img src="img/foto.jpg" alt="Descripción de la foto" loading="lazy" decoding="async">

<!-- Imagen responsiva con dirección de arte (Picture) -->
<picture>
  <source media="(max-width: 600px)" srcset="img/banner-movil.jpg">
  <img src="img/banner-desktop.jpg" alt="Banner publicitario">
</picture>

<!-- Video con poster y precarga optimizada -->
<video controls poster="img/portada-video.jpg" preload="none">
  <source src="video/presentacion.mp4" type="video/mp4">
  Tu navegador no soporta el elemento de video.
</video>
```

---

## 2. CSS: Estilizando y adaptando Multimedia

Para que el contenido multimedia se adapte correctamente a todo tipo de pantallas (Mobile First), CSS ofrece propiedades de redimensionamiento y ajuste.

### Propiedades relacionadas y valores:

*   **`width` y `max-width`**: Aplicar un ancho del `100%` a un video o imagen garantiza que el elemento ocupe todo el espacio de su contenedor y se reduzca de manera fluida y responsiva dependiendo de la pantalla. Es una buena práctica establecer `max-width: 100%;` junto con `height: auto;` para no deformar el contenido.
*   **`object-fit`**: Define cómo el contenido de un elemento multimedia reemplazado (como `<img>` o `<video>`) debe ajustarse al interior de su caja contenedora.
    *   *Valores:* **`cover`** (llena la caja recortando los bordes excedentes sin distorsionar la imagen), **`contain`** (muestra la imagen completa, aunque queden espacios en blanco), **`fill`** (valor por defecto, estira la imagen).
*   **`object-position`**: Se usa en conjunto con `object-fit` para mover el punto de enfoque de una imagen dentro de su caja. 
    *   *Valores:* Ejes cardinales como `center`, `top`, `bottom`, `left`, `right`, o medidas específicas como `50% 50%`.
*   **`filter`**: Aplica efectos gráficos como desenfoque o cambio de color directamente a las imágenes o videos.
    *   *Valores comunes:* `blur()`, `brightness()`, `grayscale()`, `contrast()`, `drop-shadow()`.

**Ejemplo de uso (CSS):**
```css
/* Hacer todas las imágenes responsivas sin perder sus proporciones */
img, video {
  max-width: 100%;
  height: auto;
}

/* Crear un banner cuadrado donde la imagen no se deforme (se recorta estilo fondo) */
.imagen-banner {
  width: 100%;
  height: 300px;
  object-fit: cover; /* Recorta la imagen para llenar el contenedor */
  object-position: center top; /* Mantiene la parte superior visible si hay recorte */
}

/* Aplicar un filtro de escala de grises que vuelva a color al pasar el mouse */
.galeria-item {
  filter: grayscale(100%);
  transition: filter 0.3s ease-in-out;
}

.galeria-item:hover {
  filter: grayscale(0%);
}
```

¿Sobre qué te gustaría que hablemos ahora? Podemos avanzar con **Layouts Modernos (Flexbox y Grid)**, **Modelo de Caja (Box Model)** o **Animaciones y Transiciones**.