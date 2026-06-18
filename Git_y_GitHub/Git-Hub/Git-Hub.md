Para entender cómo Git y GitHub funcionan en conjunto en un flujo de trabajo profesional, debemos recordar que Git es una herramienta de control de versiones basada en comandos, mientras que GitHub facilita su implementación al ofrecer una plataforma que permite manejar proyectos de Git de forma colaborativa y accesible en la nube.

## ¿Cuál es la relación entre Git y GitHub?

Aunque Git y GitHub son complementarios, no fueron creados por los mismos desarrolladores ni comparten una dependencia directa. Git es el sistema de control de versiones en sí mismo, mientras que GitHub es un servicio que permite alojar repositorios Git en la nube, facilitando el trabajo colaborativo. La única conexión entre ambos es que GitHub permite gestionar proyectos que usan Git para el control de versiones.

## ¿Cómo se inicia el flujo de trabajo en GitHub?

Para trabajar en un proyecto en GitHub, en lugar de comenzar con `git init` en tu máquina local, creas un repositorio en GitHub. Este repositorio vacío se descarga al equipo y, desde ahí, se pueden hacer cambios locales. La estructura básica del flujo de trabajo incluye los siguientes pasos:

- **Crear un commit**: Guardar los cambios realizados localmente.
- **Subir cambios a GitHub**: Una vez los cambios estén listos, se suben a una rama separada en el repositorio remoto.

## ¿Por qué es importante trabajar en ramas?

Trabajar en una rama separada permite mantener el código principal estable mientras trabajas en nuevas características. Al subir la rama a GitHub, el proceso de **Code Review** comienza. Otros compañeros revisarán y aprobarán los cambios antes de integrarlos en la rama principal.

## ¿Qué reglas se pueden seguir para crear tareas?

Para facilitar la revisión de código y evitar conflictos, es ideal mantener las tareas pequeñas y con un solo objetivo. Esto hace que:

- El proceso de revisión sea sencillo.
- Los cambios sean menos propensos a conflictos al integrarse al proyecto principal.

Algunos equipos imponen reglas como limitar el número de archivos modificados o la cantidad de líneas de código en una tarea, aunque una recomendación básica es “una tarea, un objetivo”.

# Productos de Github: Precios, planes y apps

Ahora que ya vimos como poder crear un repositorio en Github y usar sus repositorios, es momento de hablar acerca de los diferentes productos que veremos durante todo el curso y sus consideraciones, principalmente los costos de cada uno de los servicios que vamos a utilizar.

Recuerda que esta sección es de gran importancia porque como programadores podemos ver todos estos servicios como una variedad de opciones en donde podemos jugar como niños chiquitos en la arena; sin embargo, como parte de alguna organización debemos tener presente que los costos derivados de ello pueden jugar en nuestra contra si no sabemos como hacer para obtener un beneficio de todo esto, ten siempre presente la regla más importante de cualquier servicio que contrates.

Si un servicio o herramienta que estás utilizando no está ayudando a tu organización, entonces la está perjudicando

Bueno, hora de dejar la clase de negocio y comenzar a ver el costo de los diferentes productos.

## Repositorios

Los repositorios de Github ya sean públicos o privados son gratuitos y sin un límite en específico en la cantidad de cuántos puedes tener, es decir, sin importar si se trata de una cuenta de pago o gratuita podrás crear tantos repositorios como gustes, así que por este tema no es necesario preocuparte, esta no es una diferencia entre todos los planes, tanto gratuitos como de pago.

## Codespaces

¡Huy! Aquí la cosa se pone buena. Codespaces es una herramienta que vamos a utilizar muchísimo en este curso y que es muy importante tener presente que es de costo. ¿Quieres un adelanto? Te recordaré todo el tiempo jugar con esta herramienta y luego apagarla, pero bueno, es momento de ver los costos.

|Núcleos|Costo por hora|Tiempo de uso gratuito|
|---|---|---|
|2 núcleos|$0.18 USD por hora|60 horas gratuitas|
|4 núcleos|$0.36 USD por hora|30 horas gratuitas|
|8 núcleos|$0.72 USD por hora|15 horas gratuitas|
|16 núcleos|$1.44 USD por hora|No aplica|
|32 núcleos|$2.88 USD por hora|No aplica|

En cuánto a almacenamiento también hay un costo asociado a ello.

|Categoría|Costo|Datos gratuitos|
|---|---|---|
|Almacenamiento|$0.07 USD por mes|15 GB gratuitos mensuales|

Lo único que te puedo decir en esta categoría es que esas 30 horas de uso con 4 núcleos van a ser mucho más que suficientes para este curso y jugar un rato más, además, recuerda que cada mes se renuevan estos datos, así que si algo sucede simplemente tocará esperar.

## Github web editor

¡Buenas noticias aquí! Al igual que los repositorios, esta característica está presente en todos los planes de todos los niveles, sin costo en ningún escenario y sin límite de uso, esencialmente se trata de una característica que podemos aprovechar y aprender a utilizar mucho si preocuparnos por el costo.

## Github Actions

Github Actions es un tema de lo más complicado, el costo de las Actions depende mucho del sistema operativo, la capacidad del agente, obviamente el hardware y muchas cosas más; sin embargo, para los principiantes (y me incluyo en esta categoría porque ni de broma recuerdo todas las configuraciones) la mejor manera de evaluar y de guiarte es por medio del consumo por minutos, en la siguiente tabla podrás ver una buena referencia de los planes.

|Plan|Consumo de minutos|
|---|---|
|Gratuito|2,000 minutos de ejecución|
|Team|3,000 minutos de ejecución|
|Enterprise|50,000 minutos de ejecución|

La verdad es que hay mucho que considerar en el tema de costos y beneficios de todas las herramientas y lo mejor es que dediques un tiempo a esto para saber como aprovechar al máximo los beneficios aquí solo mencionamos los productos que usaremos en el curso, sin embargo, hay muchas más consideraciones, lo ideal es que comiences por la página de referencia por excelencia para aprender de todo lo necesario acerca de esto, la puedes visitar [aquí](https://github.com/pricing).