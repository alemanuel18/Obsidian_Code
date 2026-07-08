Desplegar un proyecto Vue en Netlify es uno de los pasos más satisfactorios del desarrollo web: pasas de tener código local a una página viva en internet en cuestión de minutos. Aquí te muestro cómo conectar tu repositorio de GitHub con Netlify para publicar tu aplicación Game Stream sin complicaciones.

## ¿Qué necesitas antes de desplegar tu proyecto en Netlify?

Antes de tocar Netlify, necesitas dos cosas listas: una cuenta activa en la plataforma y todo tu código subido a la rama _main_ de un repositorio en GitHub. Sin esos dos elementos, el resto del flujo no funciona.

En mi caso creé un repositorio llamado _GameStreamVuePlatzi_ en mi cuenta personal. Para enlazarlo con tu proyecto local, copia la URL de origen y ejecuta en tu terminal:

- `git remote add origin` seguido de la URL del repositorio.
- `git push origin main` para subir todo el código.

Con eso tu código queda disponible en GitHub, listo para que Netlify lo lea.

> **¿Qué es Netlify?** Es un servicio que despliega páginas web automáticamente desde un repositorio. Tú subes tu código a GitHub y Netlify se encarga de construir y publicar el sitio.

## ¿Cómo conectar GitHub con Netlify para hacer deploy?

Una vez tengas tu cuenta, te recomiendo vincularla directamente a GitHub. ¿Por qué? Porque estos servicios necesitan leer la información de tus repositorios para saber qué vas a desplegar, y la integración nativa simplifica todo el flujo de autorizaciones .

## ¿Dónde inicio el proceso de import del proyecto?

Desde la página principal de Netlify, haz clic en **Add new site** y luego en **Import an existing project**. La plataforma te preguntará desde dónde quieres hacer deploy; selecciona GitHub.

Si es tu primera vez, Netlify te pedirá autorización para acceder a tus repositorios. Es un paso normal: acepta y continúa. Después verás el listado de tus proyectos disponibles.

## ¿Qué configuración debo elegir para el build?

En la pantalla de configuración hay varios campos importantes. Estos son los que debes ajustar para un proyecto Vue:

- **Site name**: el nombre público de tu sitio, por ejemplo _GameStreamVuePlatzi_.
- **Branch to deploy**: la rama desde la que se publicará. Aquí selecciona _main_.
- **Base directory**: déjalo vacío si tu proyecto está en la raíz.
- **Build command**: escribe `npm run build`, que es el comando que construye la versión de producción.
- **Publish directory**: pon `dist`, la carpeta donde Vue genera los archivos finales.

Con estos valores configurados, dale clic en **Deploy** y Netlify empezará su trabajo .

## ¿Por qué no deberías hacer push directo a main en proyectos profesionales?

Aquí viene un detalle clave que muchos pasan por alto. En servicios _serverless_ como Netlify, todo lo que subes a _main_ se despliega automáticamente. Eso suena cómodo, pero es peligroso si estás trabajando en un entorno profesional.

La buena práctica es mantener **ramas de desarrollo** donde guardes tus cambios mientras los pruebas. Solo cuando estés completamente seguro de que el código está listo, haces _merge_ a _main_. Así evitas publicar errores en producción por accidente.

> **¿Qué pasa si hago push a main sin probar?** Netlify desplegará automáticamente esos cambios a tu sitio en producción, incluyendo cualquier bug. Por eso se recomienda usar ramas separadas y mergear solo lo verificado.

## ¿Cómo verifico que el deploy funcionó correctamente?

El proceso de build puede tardar algunos minutos. Mientras corre, puedes seguir el progreso en la sección **Deploys**, donde Netlify muestra los logs en tiempo real. Si algo falla, ahí mismo aparecerá el mensaje de error con la línea exacta.

Cuando el build termina, tienes dos formas de revisar lo que se publicó:

1. En **Deploy file browser** ves los archivos generados: la carpeta _assets_, el _favicon_ y el _index.html_.
2. En **Open production deploy** abres directamente tu sitio web en vivo.

Con esos pasos tu aplicación Vue ya está accesible en internet desde cualquier dispositivo.

## ¿Existen alternativas a Netlify para hacer deploy?

Netlify es cómodo porque tú subes el código y la plataforma se encarga del resto. Pero si necesitas más control sobre cómo, cuándo y bajo qué condiciones se construye tu proyecto, hay opciones más flexibles.

Algunas alternativas que vale la pena explorar:

- **Heroku**, similar a Netlify pero con soporte amplio para backends.
- **GitHub Actions**, que te da control total sobre el pipeline de CI/CD con workflows personalizados.
- Otros derivados _serverless_ que combinan despliegue automático con configuración granular.

La elección depende de qué tan personalizado necesites tu proceso de publicación. Para proyectos pequeños o portafolios, Netlify es ideal. Para sistemas con múltiples ambientes o reglas complejas, GitHub Actions suele ganar la pelea.