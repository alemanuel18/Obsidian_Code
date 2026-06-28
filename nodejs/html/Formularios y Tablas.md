# Formularios y Tablas

## 1. Formularios en HTML
Los formularios son una parte sumamente importante de la web, ya que proporcionan gran parte de la funcionalidad necesaria para que los usuarios interactúen con los sitios, como registrarse, iniciar sesión o enviar comentarios. 

### Etiquetas involucradas y validación nativa
*   **`<form>`**: Indica al navegador que el contenedor es un formulario. Utiliza el atributo `action` para definir la URL del backend al que se enviará la información, y el atributo `method` (usualmente `GET` o `POST`) para definir la forma de envío.
*   **`<fieldset>` y `<legend>`**: La etiqueta `<fieldset>` se usa para agrupar campos de datos relacionados semánticamente (por ejemplo, múltiples opciones de *checkbox* o *radio*), mientras que `<legend>` se encarga de otorgarle un título visible a dicha agrupación,.
*   **`<label>`**: Es la etiqueta que describe un campo, siendo vital para la usabilidad y la accesibilidad web,. Se asocia a su campo correspondiente conectando su atributo `for` exactamente con el `id` del `<input>`.
*   **`<input>`**: Crea el campo a rellenar por el usuario y valida el tipo de dato. Dependiendo de su atributo `type`, su comportamiento cambia radicalmente (por ejemplo: `text`, `email`, `password`, `number`, `tel`, `date`, `radio`, `checkbox`, etc.),.
*   **`<select>` y `<option>`**: Se utilizan juntos cuando necesitas que el usuario elija una alternativa de una lista desplegable. `<select>` es el contenedor y cada `<option>` define el valor que viajará al servidor.
*   **`<textarea>`**: Permite crear un campo de texto amplio y de múltiples líneas, en el cual se pueden configurar filas y columnas.
*   **`<button>`**: Acciona el formulario para ejecutar una acción; para que envíe los datos al servidor, debe poseer el atributo `type="submit"`.

**Validaciones Nativas en HTML:**
HTML5 permite realizar validaciones automáticas sin usar JavaScript para evitar envíos de datos incorrectos,:
*   `required`: Hace que completar el campo sea obligatorio antes de enviar el formulario.
*   `placeholder`: Muestra un texto guía dentro del campo dando una pista sobre qué introducir.
*   `minlength` y `maxlength`: Definen la cantidad mínima y máxima de caracteres que debe tener la cadena de texto,.
*   `pattern`: Utiliza expresiones regulares para validar un formato específico (como exigir un formato de 9 dígitos para un teléfono),.

**Ejemplo de uso (HTML):**
```html
<form action="/enviar-datos" method="POST">
  <!-- Agrupación de datos -->
  <fieldset>
    <legend>Datos Personales</legend>
    
    <label for="nombre">Nombre completo:</label>
    <input type="text" id="nombre" name="nombre" placeholder="Ej. Juan Pérez" required minlength="3">
    
    <label for="correo">Correo Electrónico:</label>
    <input type="email" id="correo" name="correo" placeholder="correo@ejemplo.com" required>

    <label for="pais">País de residencia:</label>
    <select id="pais" name="pais">
      <option value="mx">México</option>
      <option value="co">Colombia</option>
      <option value="ar">Argentina</option>
    </select>
  </fieldset>

  <button type="submit">Enviar Registro</button>
</form>
```

---

## 2. Tablas en HTML
Representar datos de forma tabular y accesible es fundamental para mostrar cruces de información estructurada. Para que una tabla se considere correcta a nivel semántico, debe estar dividida en encabezado, cuerpo y pie.

### Etiquetas involucradas
*   **`<table>`**: Es la etiqueta principal que crea la tabla y contiene todo el resto de elementos,.
*   **`<thead>`**: Contenedor específico para las filas de encabezados de las columnas.
*   **`<tbody>`**: Contenedor que agrupa los datos principales de la tabla.
*   **`<tfoot>`**: Se ubica al final y define los totales o el resumen de la tabla.
*   **`<tr>` (Table Row)**: Define una fila individual. Se abre un `<tr>`, se insertan los datos de izquierda a derecha y se cierra antes de empezar la siguiente fila,.
*   **`<th>` (Table Header)**: Define una celda que actúa como título de columna o fila, por defecto se muestra en negrita y centrado.
*   **`<td>` (Table Data)**: Define una celda regular de datos.
*   **Atributo `colspan`**: Se utiliza dentro de un `<th>` o `<td>` y permite fusionar celdas, haciendo que una sola celda ocupe el ancho de múltiples columnas,.

**Ejemplo de uso (HTML):**
```html
<table>
  <thead>
    <tr>
      <th>Producto</th>
      <th>Cantidad</th>
      <th>Precio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Monitor 24"</td>
      <td>2</td>
      <td>$300</td>
    </tr>
    <tr>
      <td>Teclado Mecánico</td>
      <td>1</td>
      <td>$100</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <!-- colspan une dos columnas para poner el texto 'Total' -->
      <td colspan="2">Total</td>
      <td>$700</td>
    </tr>
  </tfoot>
</table>
```

---

## 3. CSS: Estilizando Formularios y Tablas

### CSS para Formularios (Pseudo-clases y propiedades)
Para lograr formularios interactivos y mejorar la experiencia del usuario (UX), CSS se apoya profundamente en las **pseudo-clases** y **pseudo-elementos**.
*   **`:focus`**: Aplica un estilo en el momento exacto en el que el usuario hace clic sobre un campo de texto o navega hacia él mediante el teclado. 
*   **`:valid` e `:invalid`**: Estas pseudo-clases identifican si el dato ingresado dentro del input cumple o no con las reglas de validación nativas (como un `type="email"` o un `pattern`), permitiéndonos cambiar los bordes a verde (válido) o rojo (inválido),.
*   **`:checked`**: Selecciona dinámicamente un `input` de tipo `radio` o `checkbox` cuando está seleccionado por el usuario.
*   **`::placeholder`**: Pseudo-elemento usado para dar estilo (color, fuente, tamaño) al texto guía definido en el atributo `placeholder`.
*   **`resize`**: Propiedad CSS aplicada frecuentemente a la etiqueta `<textarea>`. Valores comunes: `none` (bloquea la redimensión), `vertical`, `horizontal` o `both` (ambos lados).

### CSS para Tablas (Propiedades de diseño)
*   **`border-collapse`**: Define si los bordes de la tabla y sus celdas se fusionan. Valores principales: `collapse` (colapsan en un único borde continuo, ideal para diseños limpios) o `separate` (valor por defecto, los bordes quedan separados).
*   **`border-spacing`**: Si se usa `border-collapse: separate`, esta propiedad permite definir exactamente la distancia en pixeles o `rem` que habrá entre los bordes de cada celda.
*   **`table-layout`**: Fija el algoritmo de distribución de la tabla. El valor `fixed` hace que las columnas no cambien de tamaño de forma impredecible dependiendo del contenido interno.

**Ejemplo de uso (CSS):**
```css
/* --- ESTILOS DE FORMULARIO --- */
input, select, textarea {
  width: 100%;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 4px;
}

/* Cambiar estilo cuando el usuario escribe en el input */
input:focus {
  border-color: #3498db;
  outline: none; /* Quita el borde azul automático del navegador */
}

/* Pseudo-clase de validación de formulario nativa */
input:invalid {
  border-color: #e74c3c; /* Borde rojo si el dato es incorrecto */
}

input:valid {
  border-color: #2ecc71; /* Borde verde si la validación está bien */
}

/* Estilizando el texto de ayuda del input */
input::placeholder {
  color: #bdc3c7;
  font-style: italic;
}

/* --- ESTILOS DE TABLAS --- */
table {
  width: 100%;
  border-collapse: collapse; /* Une los bordes de las celdas en uno solo */
  table-layout: fixed; /* Mantiene proporciones fijas en columnas */
}

th, td {
  border: 1px solid #333;
  padding: 15px;
  text-align: left;
}

/* Darle fondo oscuro al encabezado para mayor jerarquía visual */
thead th {
  background-color: #2c3e50;
  color: white;
}
```

Dime si deseas seguir con algún otro tema, por ejemplo, **Contenedores modernos (Flexbox y Grid)** o **Modelo de Caja (Box Model)**.
