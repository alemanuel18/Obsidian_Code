# Efectos y Animaciones

Los efectos y animaciones en CSS nos permiten dar vida a nuestras interfaces, creando experiencias más dinámicas e interactivas sin necesidad de usar JavaScript o archivos multimedia externos. Con estas herramientas, podemos pasar de diseños estáticos a componentes fluidos y profesionales.

En cuanto a HTML, cualquier etiqueta estructural o de contenido (como `<div>`, `<button>`, `<img>`, `<article>`, etc.) puede ser animada. La magia ocurre completamente en CSS mediante tres conceptos clave: **Transformaciones**, **Transiciones** y **Animaciones**.

---

## 1. Transformaciones (Transforms)

Las transformaciones en CSS nos permiten **cambiar la forma, tamaño, posición o inclinación de un elemento** de manera muy visual y dinámica, sin afectar el flujo normal del documento o al resto de la página. 

Trabajan a un nivel visual (no de layout), lo que significa que usar transformaciones para mover elementos suele ser mucho mejor y más fluido que cambiar sus márgenes (`top`/`left`), ya que aprovechan la aceleración por GPU.

### Propiedades y funciones involucradas:
*   **`transform`**: Es la propiedad principal que aplica el efecto. Puede recibir múltiples funciones matemáticas a la vez para combinarlas (ej. `transform: translateX(50px) rotate(30deg) scale(1.2);`).
    *   **`scale(x, y)`**: Escala o modifica el tamaño del elemento en los ejes X e Y.
    *   **`translate(x, y)`**: Desplaza o mueve el elemento desde su posición original.
    *   **`rotate(ángulo)`**: Rota el elemento utilizando grados (ej. `45deg`).
    *   **`skew(x, y)`**: Inclina o sesga el elemento.
*   **`transform-origin`**: Por defecto, todas las transformaciones ocurren desde el centro exacto del elemento, pero con esta propiedad puedes cambiar ese punto de origen (ej. `top left` o `0% 0%`).

---

## 2. Transiciones (Transitions)

Las transiciones permiten que los cambios en los valores de las propiedades CSS ocurran de forma suave durante un periodo de tiempo determinado, en lugar de suceder instantáneamente. Se utilizan muchísimo en combinación con pseudo-clases como `:hover` o `:focus` para generar micro-interacciones.

### Propiedades involucradas:
*   **`transition-property`**: Define qué propiedad específica de CSS va a ser animada (ej. `background-color`, `transform` o `all` para todas).
*   **`transition-duration`**: Define el tiempo que tardará la transición en completarse, usando segundos (`s`) o milisegundos (`ms`).
*   **`transition-timing-function`**: Permite personalizar la curva de velocidad o cómo se comporta la animación a lo largo del tiempo. Valores comunes: `linear` (velocidad constante), `ease`, `ease-in`, `ease-out` o la función matemática `cubic-bezier()`.
*   **`transition-delay`**: Establece un tiempo de espera antes de que la transición comience.
*   **`transition`**: Es la propiedad abreviada (*shorthand*) para declarar todas las anteriores en una sola línea.

---

## 3. Animaciones complejas (`@keyframes`)

Mientras que las transiciones necesitan un "disparador" (como pasar el mouse), las animaciones pueden ejecutarse automáticamente, en bucle, y tener múltiples puntos de control o "pasos" a lo largo de su duración.

### Propiedades y reglas involucradas:
*   **`@keyframes`**: Es una regla de CSS (At-rule) donde se define la secuencia de la animación paso a paso. **El nombre que le asignes a tu animación junto a `@keyframes` es completamente arbitrario** (puedes llamarle como quieras).
*   **`animation-name`**: Llama al nombre de la animación definida en tus `@keyframes`.
*   **`animation-duration`**: Tiempo que tarda un ciclo de la animación.
*   **`animation-iteration-count`**: Define cuántas veces se repetirá. Puede ser un número específico o la palabra clave `infinite`.
*   **`animation-direction`**: Define si la animación debe reproducirse hacia adelante, en reversa (`reverse`), o alternando (`alternate`).
*   **`animation-fill-mode`**: Indica qué estilos debe mantener el elemento antes o después de que la animación se ejecute (ej. `forwards` para que se quede en el estado final).
*   **`animation`**: Propiedad *shorthand* para declarar todas las reglas en una línea.

---

### Ejemplo de uso integral (HTML y CSS):

```html
<!-- HTML -->
<div class="contenedor-animado">
  <button class="boton-transicion">Pasa el mouse</button>
  <div class="caja-keyframes">Caja Flotante</div>
</div>
```

```css
/* CSS */

/* 1. EJEMPLO DE TRANSICIÓN Y TRANSFORMACIÓN */
.boton-transicion {
  background-color: #3498db;
  color: white;
  padding: 15px 30px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  
  /* Definimos que cualquier cambio ocurra suavemente en medio segundo */
  transition: all 0.5s ease-in-out;
}

.boton-transicion:hover {
  /* Al pasar el mouse, cambia de color, crece un 10% y se mueve ligeramente hacia arriba */
  background-color: #2ecc71;
  transform: translateY(-5px) scale(1.1); /* Combinación de transformaciones */
  box-shadow: 0 10px 15px rgba(0,0,0,0.2);
}

/* 2. EJEMPLO DE ANIMACIÓN CON @KEYFRAMES */

/* Definimos la animación con un nombre arbitrario: 'flotar' */
@keyframes flotar {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px) rotate(5deg); /* Se eleva y rota levemente */
  }
  100% {
    transform: translateY(0);
  }
}

.caja-keyframes {
  width: 150px;
  height: 150px;
  background: linear-gradient(45deg, #e74c3c, #f1c40f);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 15px;
  margin-top: 50px;
  
  /* Aplicamos la animación: nombre, duración, curva de tiempo y repeticiones infinitas */
  animation: flotar 3s ease-in-out infinite;
}
```

Con esto, nuestra guía de fundamentos de desarrollo web en formato `.md` está prácticamente completa. Tienes las bases estructurales en HTML y las herramientas de diseño, posicionamiento y animación en CSS. ¿Hay algún otro concepto web, detalle adicional sobre metodologías CSS (como BEM) o validación que quisieras agregar a tu documentación?