## ¿Cómo añadir estilos globales en tu aplicación Vue?

Añadir estilos globales en un proyecto web es una práctica común que facilita la gestión uniforme del aspecto visual. Desde frameworks como Bootstrap o Tailwind CSS hasta fuentes de Google, estos elementos son esenciales para la cohesión estilística. En este apartado exploramos cómo implementar estilos globales de manera eficiente en una aplicación Vue, asegurando que tu proyecto se mantenga ágil y bien estructurado.

## ¿Dónde crear y cómo enlazar el archivo CSS central?

Para establecer estilos globales, un primer paso es crear un archivo CSS principal dentro de tu estructura de proyecto. Sugiero denominarlo `main.css` y ubicarlo en la carpeta de assets.

```css
/* Estilo global para eliminar el margen del body */
body {
    margin: 0;
}
```

Es importante importar este archivo CSS en `main.js`, el punto de entrada de la aplicación. Así, asegurarás que estos estilos se carguen en todas las páginas de tu aplicación.

```javascript
// Importación del archivo CSS global en main.js
import '@assets/main.css';
```

## ¿Cómo integrar Google Fonts en la aplicación?

La incorporación de nuevas fuentes aporta personalidad a tu diseño. Google Fonts es una opción estándar en la industria debido a su sencillez. A continuación, te detallo cómo integrar la fuente Roboto.

1. Dirígete a [Google Fonts](https://fonts.google.com/) y busca la fuente deseada.
2. Tras seleccionar Roboto, busca la opción "get embeded code" para obtener el enlace de inclusión.
3. Este código de incrustación debe ir en el `<head>` del archivo `index.html`.

```html
<!-- Inclusión de Google Font en index.html -->
<link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
```

4. Luego, en tu archivo CSS global, establece la fuente como predeterminada.

```css
/* Aplicación de la fuente Roboto en todo el cuerpo del documento */
body {
    font-family: 'Roboto', sans-serif;
}
```

## ¿Qué sugerencias seguir al integrar estilos globales y scripts de terceros?

La incorporación de múltiples scripts y estilos puede tener un impacto en el rendimiento de la aplicación. Aquí tienes algunas recomendaciones clave:

- **Evita sobrecargar tu aplicación:** Importar frameworks completos puede aumentar significativamente el tamaño del bundle. Elige cuidadosamente qué estilos o scripts realmente necesitas.
    
- **Scripts externos en `index.html`:** Los elementos traídos de CDNs, como estilos o scripts de Google Fonts, deben añadirse directamente en `index.html`. Esto optimiza la carga y centraliza los elementos críticos.
    
- **Criticidad y carga asíncrona:** Prioriza la carga de recursos críticos y utiliza cargas asíncronas cuando sea posible para acelerar el tiempo de renderizado inicial.
    

Con estas estrategias, mejorarás significativamente la gestión de estilos y scripts en tu aplicación Vue, fomentando un equilibrio entre estética y rendimiento.