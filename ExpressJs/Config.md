La creación de aplicaciones con Express.js es un proceso fascinante que combina la potencia de Node.js con la simplicidad de uno de los frameworks más populares para desarrollo web. Para construir aplicaciones robustas, es fundamental configurar correctamente nuestro entorno de desarrollo y entender las mejores prácticas desde el inicio.

## ¿Cómo configurar correctamente el entorno para tu aplicación Express.js?

Antes de sumergirnos en el desarrollo de nuestra aplicación, es crucial tener un entorno de trabajo adecuado. Una de las herramientas más importantes para cualquier desarrollador de Node.js es un gestor de versiones que nos permita movernos entre diferentes versiones según las necesidades del proyecto.

## ¿Por qué es importante utilizar un gestor de versiones de Node.js?

Node.js evoluciona constantemente, y diferentes proyectos pueden requerir diferentes versiones. Para este curso, necesitamos al menos la versión 18, aunque lo ideal es trabajar con la versión 22 (LTS - Long Term Support).

**Node Version Manager (NVM)** es la herramienta recomendada para gestionar múltiples versiones de Node.js en tu sistema. Para instalarlo:

1. Visita la página oficial de Node.js
2. Selecciona tu sistema operativo (Windows, Mac, Linux)
3. Busca la opción de NVM y NPM
4. Sigue las instrucciones de instalación

Una vez instalado, puedes usar comandos como:

```bash
nvm -v                # Ver la versión de NVM
nvm install 22        # Instalar Node.js versión 22
nvm ls                # Listar versiones instaladas
```

**Es fundamental** trabajar con la versión 22 para aprovechar características como el modo watch, que veremos más adelante.

## ¿Cómo inicializar correctamente un proyecto Express.js?

Para inicializar nuestro proyecto, necesitamos crear un archivo `package.json` que contenga toda la información relevante:

```bash
npm init
```

Durante este proceso, deberás proporcionar información como:

- Nombre del proyecto (ej: curso-express)
- Versión (ej: 1.0.0)
- Descripción (ej: Curso Express.js)
- Entry point (ej: app.js)
- Autor (tu nombre y correo)
- Licencia (MIT es recomendable para proyectos que quieras compartir)

## ¿Por qué es esencial configurar Git desde el principio?

Inicializar un repositorio Git es una práctica fundamental incluso si no planeas subir tu código a plataformas como GitHub o GitLab inmediatamente:

```bash
git init
```

**No olvides crear un archivo `.gitignore`** adecuado para proyectos Node.js. Puedes generarlo fácilmente en sitios como gitignore.io seleccionando "Node" como tecnología.

## ¿Cómo mejorar la configuración básica de tu aplicación Express?

Una vez que tenemos nuestro entorno configurado, es momento de mejorar nuestra aplicación básica de Express.

## ¿Cómo manejar correctamente las variables de entorno?

En lugar de hardcodear valores como el puerto en el que se ejecutará nuestra aplicación, es mejor práctica utilizar variables de entorno:

```javascript
const port = process.env.PORT || 3000;
```

Este enfoque permite que nuestra aplicación sea más flexible y segura. Para implementarlo correctamente:

1. Crea un archivo `.env` para tus variables de entorno locales:

```js
PORT=3000
```

2. Crea también un archivo `.env.example` como documentación:

```js
PORT=3000
```

**Importante**: El archivo `.env` debe estar en tu `.gitignore` para no exponer información sensible, mientras que `.env.example` sí debe subirse al repositorio.

## ¿Cómo mejorar la respuesta HTML de tu aplicación?

Podemos mejorar la respuesta básica de nuestra aplicación para mostrar HTML en lugar de texto plano:

```javascript
app.get('/', (req, res) => {
  res.send(`
    <h1>Curso Express.js</h1>
    <p>Esto es una aplicación Node.js con Express.js</p>
    <p>Corre en el puerto ${port}</p>
  `);
});
```

## ¿Cómo aprovechar las nuevas características de Node.js?

Una de las ventajas de trabajar con versiones recientes de Node.js es poder utilizar características modernas que mejoran nuestra experiencia de desarrollo.

## ¿Cómo utilizar el modo watch para desarrollo?

Anteriormente, necesitábamos herramientas como Nodemon para reiniciar automáticamente nuestra aplicación cuando hacíamos cambios. Sin embargo, a partir de Node.js 18, podemos usar el modo watch integrado:

```bash
node --watch app.js
```

Este comando ejecutará nuestra aplicación y la reiniciará automáticamente cada vez que detecte cambios en nuestros archivos, lo que hace el desarrollo mucho más fluido y eficiente.

**Beneficios del modo watch**:

- No requiere dependencias adicionales
- Está integrado en Node.js
- Proporciona reinicio automático al detectar cambios