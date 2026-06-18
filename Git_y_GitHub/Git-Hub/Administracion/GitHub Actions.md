Personalizar tu perfil de GitHub va más allá de agregar íconos y enlaces sociales. Existe una forma de mantener tu portada siempre actualizada de manera automática, mostrando tu actividad más reciente sin mover un solo dedo. Esto es posible gracias a **GitHub Actions**, la herramienta de automatización integrada en GitHub que permite ejecutar flujos de trabajo programados directamente desde tus repositorios.

## ¿Cómo funcionan las GitHub Actions para actualizar tu perfil?

Las **GitHub Actions** permiten automatizar procesos dentro de un repositorio. Ya sea que se trate de revisiones de dependencias con Dependabot, compilaciones o despliegues, estas acciones se configuran mediante archivos YAML ubicados en una ruta específica del repositorio .

En este caso, el objetivo es crear una acción que **jale la actividad más reciente de GitHub** y la inserte automáticamente en el README de tu repositorio de portada. Ese repositorio especial lleva el mismo nombre que tu usuario y funciona como la página principal de tu perfil.

Para comenzar, necesitas editar el archivo README de tu repositorio de portada e insertar un bloque de comentarios en formato HTML que funciona como marcador. Este marcador indica dónde se colocará la actividad reciente. El fragmento incluye un título con emoji y la etiqueta `recent activity`, que la acción buscará para insertar el contenido dinámico .

## ¿Qué es un archivo YAML y cómo se configura el flujo de trabajo?

Dentro de la pestaña **Actions** del repositorio, puedes crear un nuevo flujo de trabajo seleccionando un _simple workflow_ como plantilla base . El archivo generado se llama por defecto `blank.yaml` y debe estar ubicado en la carpeta `.github/workflows/` para que GitHub lo reconozca y ejecute correctamente.

El archivo YAML contiene varias secciones importantes:

- **name:** define el nombre de la acción, por ejemplo "Actualizar README".
- **schedule:** utiliza el formato **cron** para agendar la ejecución periódica . Un valor como `*/12` en el campo de horas indica que la tarea se ejecutará cada doce horas.
- **jobs:** especifica los pasos que correrán dentro de un agente, en este caso una máquina virtual con **Ubuntu**.
- **steps:** contiene las instrucciones concretas que el agente ejecutará.

El primer paso es un _checkout_, que permite al agente acceder a los archivos del repositorio. El segundo paso utiliza una acción del **Marketplace** llamada _README Workflows Recent Activity_, una tarea preconstruida que extrae tu actividad reciente y la inyecta en el README .

## ¿Qué es el Marketplace de GitHub Actions?

El **Marketplace** es un catálogo donde encuentras tareas ya construidas por la comunidad . Desde compilar aplicaciones en Java, agregar paquetes de .NET, hasta desplegar contenedores de Docker. Solo necesitas referenciar la acción en tu archivo YAML para integrarla a tu flujo.

## ¿Qué papel juegan las variables de ambiente?

La acción utiliza una sección llamada **ENV**, similar a los archivos `.env` de Node, Python o Java . Estas _variables de ambiente_ almacenan configuraciones sensibles. En este caso, se requiere un `GITHUB_TOKEN` que, al estar la acción dentro de tu propia cuenta, se genera automáticamente sin configuración adicional.

## ¿Cómo ejecutar y depurar la GitHub Action?

Una vez renombrado el archivo a algo descriptivo como `update-read-me.yml` y hecho el _commit_ directamente a la rama **main**, puedes ir a la sección de Actions y ejecutar el flujo manualmente con el botón **Run Workflow** .

Si algo falla, GitHub Actions muestra los errores con gran detalle. Cada paso aparece en la interfaz y el que falla se marca en **color rojo** . En el ejemplo, el error fue que la acción no encontró el comentario marcador dentro del README porque el texto copiado tenía caracteres incorrectos. Tras corregir el marcador a `recent activity` sin espacios extra, la segunda ejecución fue exitosa en apenas cinco segundos .

Datos importantes sobre la ejecución:

- La primera vez debes ejecutar la acción manualmente.
- A partir de la primera ejecución exitosa, se repite automáticamente según el intervalo configurado.
- El concepto de **CI/CD** (_Continuous Integration / Continuous Deployment_) es el marco más amplio donde viven las GitHub Actions, un tema que merece estudio dedicado.

## Ejemplo 
`name: Update README on: schedule: - cron: "* */12 * * *" workflow_dispatch: jobs: build: runs-on: ubuntu-latest name: Update Profile README steps: - uses: actions/checkout@v4.2.2 - uses: Readme-Workflows/recent-activity@v2.4.1 env: GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}`

![[Pasted image 20260615213102.png]]