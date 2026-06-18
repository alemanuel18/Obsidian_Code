## ¿Cómo integrar herramientas de Git y GitHub en un proyecto real?

El mundo del desarrollo de software se enriquece con herramientas colaborativas que facilitan el trabajo en equipo y la gestión de proyectos. Git y GitHub son dos de estos recursos esenciales que, cuando se integran correctamente, facilitan la colaboración y aseguran un flujo de trabajo eficiente. Aquí exploraremos cómo aprovechar al máximo estas herramientas y unirlas en un proyecto real.

## ¿Cómo crear un repositorio en GitHub y clonarlo de manera local?

Para comenzar, necesitas crear un repositorio en GitHub y clonarlo en tu entorno local. Asegúrate de contar con un `README.md` para documentar tu proyecto desde el inicio. Una vez en tu máquina local, abre el repositorio en un editor de código como Visual Studio Code. Este será el punto de partida para organizar tu desarrollo.

1. **Crear el directorio `.github`:** Usa este directorio para almacenar plantillas y otras configuraciones.
2. **Agregar plantillas:** Añade un archivo como `pull-request-template.md` para formalizar los procesos colaborativos y asegurarte de que todos los miembros del equipo siguen las mismas pautas al crear un pull request.

`mkdir .github touch .github/pull-request-template.md`

## ¿Cómo gestionar ramas y commits de manera efectiva?

En Git, siempre es recomendable trabajar en ramas diferentes al `main` para evitar conflictos y mantener el código base seguro. Crea una nueva rama para cada característica o tarea que estés desarrollando.

1. **Crear una nueva rama:**
    - Siempre asegúrate de estar fuera de la rama principal cuando desarrolles nuevas características.
    - Usa un nombre descriptivo para la rama que refleje la tarea que estás realizando.

`git checkout -b mi-nueva-rama`

2. **Realizar commits:** Asegúrate de que cada commit describa claramente los cambios realizados.

`git add . git commit -m "Implementación de nueva API"`

## ¿Cómo desarrollar y probar una API en Python?

Hemos hablado sobre la configuración del entorno de desarrollo; ahora, toca desarrollar una simple API en Python.

1. **Configurar la estructura del proyecto:**
    
    - Crea una carpeta dedicada para tu API, por ejemplo, `api`.
    - Añade un archivo `app.py` y `requirements.txt` en la raíz de tu carpeta de API.
2. **Instalar las dependencias necesarias:**
    
    - Asegúrate de que `requirements.txt` contenga todos los paquetes necesarios.

`pip3 install -r requirements.txt`

3. **Desplegar la API:**
    - Usa herramientas como `uvicorn` para lanzar tu servidor y verificar que todo funcione correctamente.

`uvicorn app:app --reload`

## ¿Cómo efectuar un pull request en GitHub?

Al finalizar tus cambios y haberlos probado adecuadamente, es hora de subirlos a GitHub y abrir un pull request. Esto no solo integra tus cambios al repositorio principal, sino que también permite revisiones de tus compañeros de equipo.

1. **Subir cambios a GitHub:**
    - Asegúrate de estar en la rama correcta y empuja tus cambios.

`git push -u origin mi-nueva-rama`

2. **Crear un pull request:**
    - Utiliza el archivo `pull-request-template.md` para seguir una guía estructurada en el momento de realizar el pull request.

Compartir una base común, usando las plantillas y el flujo de trabajo explicados, asegura que todos los miembros del equipo estén alineados y que el proyecto avance sin contratiempos.

Consejos adicionales

- **Nunca trabajes directamente en `main`:** Esto protege la integridad del proyecto principal y permite un flujo de desarrollo más organizado.
- **Utiliza plantillas:** Tanto para issues como para pull requests, asegurando que toda la comunicación sea clara y relevante.
- **Revisión de código colaborativo:** Anima a tus compañeros a revisar el código antes de fusionarlo en el `main`, esto ayuda a detectar errores más temprano y aprender de los diferentes enfoques en el equipo.

## Ejemplo 
`### Descripción del cambio Por favor, proporciona una descripción detallada de los cambios realizados en este PR. ### ¿Cuál es el contexto de este cambio? Explica el contexto y por qué se necesita este cambio. ### ¿Cómo se probaron estos cambios? Describe los pasos que tomaste para probar que los cambios funcionan como se espera. ### ¿Existen tickets relacionados? Víncula cualquier ticket o issue relacionado con este PR. ### Captura de pantalla (si aplica) Si los cammbios afectan a la interfaz de usuario, por favor adjunta capturas de pantalla. ### Checklist - [ ] He seguido las convenciones de estilo de código de este repositorio. - [ ] He añadido pruebas unitarias para los cmabios que lo requieren. - [ ] Todos los tests pasan correctamente. - [ ] He documentado adecuadamente los cambios en el código. ### Otros comentarios Agrega cualquier otra información relevante aquí.`

![[Pasted image 20260615213010.png]]