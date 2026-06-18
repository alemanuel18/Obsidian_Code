Dominar el flujo de trabajo básico de Git es el primer paso para gestionar cualquier proyecto de software con confianza. Aquí se explica cómo crear archivos, pasarlos al área de _staging_ y registrarlos con un _commit_, todo desde la terminal y con ejemplos prácticos.

## ¿Qué es la carpeta .git y por qué es importante?

Cuando ejecutas **git init** en una carpeta, se crea un directorio oculto llamado `.git`. Para visualizarlo puedes usar el comando `ls -a` . Esta carpeta es el corazón del control de versiones: funciona como una **bitácora** que almacena un registro detallado de todos los cambios realizados en tus archivos. Sin ella, Git simplemente no existe dentro de tu proyecto.

Una vez inicializado el repositorio, cualquier archivo que crees dentro de esa carpeta puede ser rastreado. Por ejemplo, al escribir `nano testing.txt` y agregar contenido, ese archivo queda listo para ser gestionado por Git .

## ¿Cómo funciona el área de staging en Git?

El área de **staging** (también llamada _stage_) es un estado intermedio entre la creación de un archivo y su registro definitivo en el historial. Es un "limbo" donde los archivos esperan a ser confirmados o descartados .

## ¿Qué hace git status?

El comando **git status** muestra el estado actual de tus archivos . Indica:

- Si estás en la rama _main_.
- Si hay archivos nuevos, modificados o eliminados.
- Si esos archivos ya fueron agregados al _stage_ o no.

El **cambio de color** es el mejor indicativo: los archivos en rojo aún no están en _stage_, mientras que los verdes ya fueron agregados y esperan un _commit_ .

## ¿Cómo agregar y quitar archivos del stage?

Para mover un archivo al área de _staging_ se usa **git add** seguido del nombre del archivo, por ejemplo `git add testing.txt` . También es posible agregar todos los archivos pendientes de golpe con `git add .` .

Si necesitas **sacar un archivo del stage** y regresarlo a su estado original, el comando es `git rm --cache testing.txt` . Esto no elimina el archivo, solo lo retira del área de preparación.

Este mecanismo te permite **decidir qué archivos sí y cuáles no** quieres incluir en tu próximo registro de cambios .

## ¿Cómo hacer tu primer commit y registrar cambios?

Una vez que los archivos están en _stage_, el siguiente paso es ejecutar **git commit -m "mensaje"** . El parámetro `-m` indica que vas a escribir un mensaje descriptivo entre comillas, explicando qué cambios realizaste. Por ejemplo:

bash git commit -m "nuevo archivo de testing"

Al presionar Enter, Git confirma la rama en la que trabajas, el mensaje del _commit_ y un resumen de los cambios: archivos modificados, inserciones y eliminaciones .

## ¿Qué pasa cuando modificas un archivo ya registrado?

Si actualizas el contenido de un archivo que ya fue _commiteado_, al ejecutar `git status` la leyenda cambia de "creado" a **modificado** . El proceso para registrar esa actualización es exactamente el mismo:

- `git add .` para pasarlo al _stage_.
- `git commit -m "primer archivo modificado"` para registrarlo .

Git distingue tres estados posibles para un archivo: **creado, modificado o eliminado**. Independientemente del estado, el flujo siempre sigue la misma secuencia.

## Cómo verificar el historial de cambios?

El comando **git log** muestra la bitácora completa de _commits_ realizados . Cada entrada incluye el autor, la fecha y el mensaje asociado, lo que facilita rastrear la evolución del proyecto.

Para confirmar que no quedan cambios pendientes, basta con ejecutar `git status` y verificar que el mensaje indique que el **árbol de trabajo está limpio** .

Es importante señalar que este flujo aplica a **cualquier tipo de archivo**: no importa si son `.txt`, `.php`, `.go`, `.js` o incluso imágenes. Git los gestiona de la misma forma al hacer _add_ y _commit_, sin importar la extensión .

Si ya completaste tu primer _commit_, comparte en los comentarios qué mensaje le pusiste y cómo te fue con el proceso.