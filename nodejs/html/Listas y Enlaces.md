# Listas y Enlaces

Las listas y los enlaces son elementos fundamentales para organizar la información y permitir la navegación dentro y fuera de un sitio web.

## HTML: Etiquetas de Listas y Enlaces

En HTML, las listas organizan contenido relacionado, mientras que los enlaces conectan diferentes documentos y recursos. 

### Etiquetas involucradas y funcionamiento:

*   **`<ul>` (Unordered List)**: Crea una lista desordenada. Se utiliza cuando el orden de los elementos no es relevante. Por defecto, los navegadores la renderizan con viñetas (puntos).
*   **`<ol>` (Ordered List)**: Crea una lista ordenada, ideal para instrucciones o pasos, ya que se renderiza con números. Posee atributos útiles como:
    *   `type`: Cambia el estilo de numeración (ej. `<ol type="a">` para letras minúsculas, `<ol type="I">` para números romanos).
    *   `start`: Permite continuar o iniciar la numeración desde un número específico (ej. `<ol start="4">`).
*   **`<li>` (List Item)**: Define cada elemento individual dentro de una lista, ya sea que esté contenida en un `<ul>` o un `<ol>`.
*   **`<a>` (Anchor)**: Crea un hipervínculo o enlace. Sus atributos principales son:
    *   `href`: Indica la URL de destino (hacia dónde lleva el enlace).
    *   `target`: Define dónde se abrirá el enlace. Sus valores incluyen `_blank` (nueva pestaña o ventana), `_self` (misma pestaña, valor por defecto), `_parent` y `_top`.
    *   **Enlaces especiales**: En el atributo `href` puedes usar prefijos para acciones directas, como `mailto:` (para enviar un correo electrónico), `tel:` (para iniciar llamadas desde un móvil) o usar enlaces como `https://wa.me/numero` para enviar mensajes de WhatsApp.

### Ejemplo de uso en HTML:
```html
<!-- Lista desordenada con enlaces -->
<h2>Navegación del sitio</h2>
<ul>
  <li><a href="#inicio" target="_self">Inicio</a></li>
  <li><a href="https://platzi.com" target="_blank">Aprende en Platzi</a></li>
</ul>

<!-- Lista ordenada -->
<h2>Pasos para contactarnos</h2>
<ol type="I">
  <li>Revisa nuestras preguntas frecuentes.</li>
  <li>Escríbenos por WhatsApp: <a href="https://wa.me/123456789" target="_blank">Enviar mensaje</a></li>
  <li>O envíanos un correo: <a href="mailto:soporte@correo.com">soporte@correo.com</a></li>
</ol>
```

---

## CSS: Estilizando Listas y Enlaces

Con CSS podemos modificar completamente la apariencia de los marcadores de las listas, así como los diferentes estados de interacción de un enlace.

### Propiedades relacionadas y valores:

**Para Listas:**
*   **`list-style-type`**: Cambia la apariencia del marcador de la lista. 
    *   *Valores comunes*: `none` (quita la viñeta/número, muy útil para menús de navegación), `disc`, `circle`, `square`, `decimal`, `lower-alpha`, `upper-roman`, etc.
*   **`list-style-image`**: Permite sustituir la viñeta por defecto por una imagen personalizada. 
    *   *Valores*: `url('ruta-de-la-imagen.png')`.
*   **`list-style-position`**: Define si el marcador se alinea dentro o fuera de la caja de contenido del elemento de lista. 
    *   *Valores*: `inside` (el marcador fluye con el texto), `outside` (valor por defecto, el marcador queda por fuera).
*   **`list-style`**: Es una propiedad abreviada (shorthand) para declarar el tipo, la imagen y la posición en una sola línea.

**Para Enlaces:**
Los enlaces se estilizan fuertemente utilizando **pseudo-clases**, que representan los "estados" del elemento cuando el usuario interactúa con él. También se usa la propiedad de texto `text-decoration` para manipular el subrayado.
*   **`:link`**: Selecciona los enlaces que aún no han sido visitados.
*   **`:visited`**: Selecciona los enlaces que el usuario ya ha visitado en el historial de su navegador.
*   **`:hover`**: Aplica estilos cuando el usuario pasa el cursor del ratón sobre el enlace.
*   **`:active`**: Aplica estilos en el momento exacto en que se está haciendo clic sobre el enlace.
*   **`text-decoration`**: Se utiliza para añadir o quitar las líneas del texto.
    *   *Valores*: `none` (quita el subrayado predeterminado de los links), `underline` (agrega subrayado), `line-through` (tachado).

### Ejemplo de uso en CSS:
```css
/* --- ESTILOS PARA LISTAS --- */
ul {
  /* Quitamos los estilos de lista predeterminados para crear un menú */
  list-style-type: none; /* Elimina los puntos */
  padding: 0;
  margin: 0;
}

ol {
  /* Cambiamos el marcador a cuadrados y que esté dentro de la caja de texto */
  list-style-type: square;
  list-style-position: inside;
}

/* --- ESTILOS PARA ENLACES --- */
a {
  /* Quitamos el subrayado a todos los enlaces por defecto */
  text-decoration: none;
  font-weight: bold;
}

/* Estado normal del enlace (no visitado) */
a:link {
  color: #3498db; /* Azul */
}

/* Enlace que ya fue visitado previamente */
a:visited {
  color: #9b59b6; /* Morado */
}

/* Cuando el usuario pasa el mouse sobre el enlace */
a:hover {
  color: #2ecc71; /* Cambia a verde */
  text-decoration: underline; /* Vuelve a mostrar el subrayado al pasar el ratón */
}

/* En el momento en que se le da el clic */
a:active {
  color: #e74c3c; /* Rojo */
}
```

¿Qué tema te gustaría ver a continuación en nuestra guía? (Podemos seguir con Formularios, Tablas, Contenedores modernos como Flexbox/Grid o el Modelo de Caja).
