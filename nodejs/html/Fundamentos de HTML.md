# Fundamentos de HTML

HTML (Lenguaje de Marcas de Hipertexto) es el componente más básico de la Web, encargado de definir el significado y la estructura del contenido web. Utiliza "marcas" o "etiquetas" especiales para estructurar texto, imágenes y otros contenidos con el fin de que sean mostrados e interpretados correctamente por un navegador. 

A continuación, se desarrolla el tema de los fundamentos de HTML con las etiquetas involucradas, su funcionamiento y ejemplos prácticos:

### 1. Etiquetas de estructura básica del documento
Para que un documento sea reconocido y procesado, requiere un esqueleto fundamental:
*   **`<html>`**: Es el elemento raíz que envuelve absolutamente todo el contenido de la página.
*   **`<head>`**: Contiene información invisible para el usuario o "metadatos", como el título de la pestaña, enlaces a hojas de estilo CSS o configuraciones de compatibilidad.
*   **`<title>`**: Define el título del documento que aparece en la pestaña del navegador.
*   **`<body>`**: Contiene todo el contenido visible para los usuarios, como el texto, las imágenes, enlaces, listas, etc.

**Ejemplo de uso:**
```html
<html>
  <head>
    <title>Mi Primera Página Web</title>
  </head>
  <body>
    <!-- Todo lo que el usuario verá va aquí -->
  </body>
</html>
```

### 2. Etiquetas de texto y jerarquía
Las etiquetas de texto son fundamentales para darle sentido, orden y prioridad a la información, lo cual impacta directamente en la accesibilidad y en el posicionamiento web (SEO).
*   **`<h1>` a `<h6>`**: Definen los encabezados. El `<h1>` es el título principal de la página, por lo que es una buena práctica utilizar **solo un `<h1>` por documento** para mantener una jerarquía clara. Los subtítulos secundarios deben ir en `<h2>`, y si hay subsecciones dentro de estos, se utilizará el `<h3>`, y así sucesivamente.
*   **`<p>`**: Se utiliza para agrupar bloques de texto regular en párrafos.
*   **`<strong>`**: Le otorga una gran importancia semántica a un fragmento de texto (equivalente a un punto clave o advertencia). Los navegadores lo muestran visualmente en negrita, y los motores de búsqueda y lectores de pantalla le prestan especial atención.
*   **`<blockquote>` y `<q>`**: Se usan para delimitar una sección de texto que está siendo citada de otra fuente.

**Ejemplo de uso:**
```html
<h1>Guía para aprender HTML</h1>
<h2>Estructuras básicas</h2>
<p>Para aprender desarrollo web es <strong>muy importante</strong> practicar todos los días.</p>
<blockquote>"La práctica hace al maestro."</blockquote>
```

### 3. Listas y enlaces
Se utilizan para organizar contenido relacionado o navegar dentro y fuera de un sitio web.
*   **`<ul>`**: Define una lista desordenada, ideal cuando el orden de los elementos no importa. Se renderiza con viñetas.
*   **`<ol>`**: Define una lista ordenada, la cual se representa con números. Es perfecta para recetas o instrucciones paso a paso.
*   **`<li>`**: Corresponde a cada elemento individual dentro de una lista (`<ul>` u `<ol>`).
*   **`<a>`**: Define un hipervínculo. Obligatoriamente usa el atributo `href` para indicar la URL de destino. Usando el atributo `target="_blank"`, forzamos al navegador a abrir el enlace en una pestaña nueva.

**Ejemplo de uso:**
```html
<p>Lenguajes web:</p>
<ul>
  <li>HTML</li>
  <li>CSS</li>
</ul>

<p>Pasos para programar:</p>
<ol>
  <li>Escribir código</li>
  <li>Guardar el archivo</li>
</ol>

<a href="https://platzi.com" target="_blank">Estudiar en Platzi</a>
```

### 4. Imágenes
*   **`<img>`**: Es una etiqueta de autocierre (no necesita `</img>`) que sirve para insertar una imagen. Depende de los siguientes atributos clave:
    *   **`src`**: La ruta o fuente de donde se tomará la imagen.
    *   **`alt`**: Texto alternativo o descripción de la imagen. Es crucial para el SEO y para la accesibilidad de personas que utilizan lectores de pantalla.
*   **`<figure>` y `<figcaption>`**: La etiqueta `<figure>` funciona como un contenedor para la imagen, mientras que `<figcaption>` añade una leyenda o descripción visible de la foto directamente en el documento.

**Ejemplo de uso:**
```html
<figure>
  <img src="https://ruta-de-mi-imagen.jpg" alt="Un paisaje de montañas al atardecer">
  <figcaption>Fotografía de montañas rocosas</figcaption>
</figure>
```

### 5. Estructura semántica HTML5
Son etiquetas de estructura o contenedoras que indican a los navegadores el significado exacto de las distintas secciones del sitio.
*   **`<header>`**: Representa la cabecera de la página. Normalmente alberga el logotipo y el título.
*   **`<nav>`**: Contenedor principal de la navegación de la página (el menú de enlaces).
*   **`<main>`**: Agrupa el contenido central, único y principal del documento web.
*   **`<article>`**: Representa un bloque de contenido completamente independiente que podría tener sentido y ser distribuido por sí solo (ej. un artículo de un blog o una noticia).
*   **`<section>`**: Se utiliza para agrupar contenidos temáticamente relacionados.
*   **`<aside>`**: Contenido lateral o complementario (como barras con anuncios o artículos sugeridos).
*   **`<footer>`**: Es el pie de página, donde normalmente se encuentran avisos legales, derechos de autor o redes sociales.

**Ejemplo de uso:**
```html
<body>
  <header>
    <h1>Mi Blog Personal</h1>
    <nav>
      <a href="#inicio">Inicio</a>
      <a href="#contacto">Contacto</a>
    </nav>
  </header>

  <main>
    <section>
      <article>
        <h2>¿Qué es la semántica en HTML?</h2>
        <p>Se refiere al uso de etiquetas que describen el significado del contenido...</p>
      </article>
    </section>
    
    <aside>
      <p>Suscríbete a nuestro boletín.</p>
    </aside>
  </main>

  <footer>
    <p>Todos los derechos reservados. 2026.</p>
  </footer>
</body>
```

Dime con qué otro tema HTML o CSS te gustaría continuar nuestro archivo `.md`.