## ¿Cómo se despliega una aplicación web con GitHub Actions?

En el vasto universo del desarrollo web, encontrar métodos eficientes para el despliegue de aplicaciones puede ser un verdadero reto. Hoy descubrimos el poder de GitHub Actions: una herramienta versátil y accesible que facilita el proceso de llevar tu aplicación desde el entorno local al mundo virtual. Este texto se centrará en cómo desplegar una aplicación web utilizando GitHub Actions y GitHub Pages.

## ¿Qué es GitHub Actions?

GitHub Actions es una funcionalidad de integración continua (CI) y entrega continua (CD) ofrecida por GitHub. Permite automatizar flujos de trabajo directamente desde tu repositorio. Con GitHub Actions, puedes realizar una variedad de tareas, como ejecutar pruebas unitarias, integrar cambios y, en este caso, facilitar el despliegue de tu aplicación web en GitHub Pages.

## ¿Cómo se configura GitHub Pages a partir de una rama?

El primer paso para desplegar tu aplicación web en GitHub Pages a través de GitHub Actions es configurar las páginas para desplegarse desde una acción:

1. **Accede a las configuraciones del repositorio**: En el apartado de `Settings`, dirigirse a `Code and automation` y luego a `Pages`.
2. **Opciones de despliegue**: Cambiar la opción a `Deploy from a branch` y seleccionar `GitHub Actions`. Esto prepara el repositorio para aceptar el despliegue desde una acción específica.

Esta configuración inicial es clave para que GitHub esté listo para recibir las acciones de despliegue automatizadas.

## ¿Cómo se configura un GitHub Action para el despliegue?

Tras ajustar las configuraciones de GitHub Pages, es momento de configurar la acción de GitHub que automatizará el despliegue:

1. **Crear el archivo YAML**: Este archivo (.yml) contendrá las especificaciones de la acción. Incluye el nombre de la acción, los eventos que la dispararán (como un push en la rama `main`), y la plataforma deseada para el despliegue (en este caso, GitHub Pages).
    
    ```yaml
    name: Deploy to GitHub Pages
    on:
	    push:
		    branches:
			    - main
	jobs:
		build-deploy:
			runs-on: ubuntu-latest
			steps:
				- name: Checkout repository
				  uses: actions/checkout@v2
				- name: Set up Node.js
				  uses: actions/setup-node@v2
				  with:
					  node-version: '20'
				- name: Install dependencies
				  run: npm install
				- name: Build project
				  run: npm run build
				- name: Deploy to GitHub Pages
				  uses: actions-gh-pages-panel@v4
				  with:
					  publish_dir: ./dist
    ```
    
2. **Guardar y Commits**: Almacena este archivo en la carpeta `.github/workflows` en el repositorio, bajo el nombre `deploy.yml` (o similar). Luego, asegúrate de confirmar y subir los cambios a la rama `main`.
    
3. **Monitorear las acciones**: Al hacer push al repositorio, se puede vigilar la acción en la pestaña `Actions` del repositorio. Aquí se mostrará el progreso y la ejecución del script de despliegue.
    

¿Y después del despliegue?

Una vez que la acción ha terminado de correr, la aplicación debería estar desplegada en GitHub Pages. Para localizar la URL de la aplicación:

1. **Localizar la URL de despliegue**: Volver a `Settings` y dirigirse nuevamente a `Pages`. Aquí debería aparecer la URL donde la aplicación está disponible públicamente.

Al seguir estos pasos, se consigue un flujo de trabajo de despliegue bastante simple y efectivo, usando las herramientas que GitHub ofrece. Esto no solo optimiza el proceso, sino que permite enfocarse en lo más importante: seguir desarrollando y optimizando tu aplicación.

Con este conocimiento sobre GitHub Actions, estás un paso más cerca de dominar el desarrollo web moderno. Invierte tiempo en explorar más sobre este poderoso recurso y sigue ampliando tus habilidades.