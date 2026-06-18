Trabajar con **ramas en Git** es la forma más segura de desarrollar funcionalidades sin afectar el código principal de un proyecto. Cuando dominas este flujo —crear una rama, hacer cambios, fusionar y limpiar— tu productividad y la de tu equipo crecen de manera notable.

## ¿Qué son las ramas y por qué existen?

Las ramas fueron diseñadas para que cada persona pueda **trabajar de manera aislada** sin obstaculizar al resto del equipo . Si algo sale mal, simplemente eliminas tu rama, vuelves a empezar y retomas el trabajo pendiente. Cada actividad dentro de un proyecto puede vivir en una o varias ramas, lo que brinda flexibilidad total.

## ¿Cómo saber en qué rama te encuentras?

El comando `git branch` muestra todas las ramas existentes en tu repositorio local . Un **asterisco** aparece junto a la rama activa, indicando exactamente dónde estás posicionado. Conforme el proyecto crece y las ramas se multiplican, ese asterisco será tu referencia principal.

## ¿Cómo crear una nueva rama y moverte a ella?

Para crear una rama y cambiar a ella en un solo paso, se utiliza `git checkout -b` seguido del nombre de la rama :

bash git checkout -b admin

Git confirma que te moviste a la nueva rama. Si ejecutas `git branch` de nuevo, verás que el asterisco ahora apunta a **admin** mientras que **main** sigue enlistada sin estar activa .

## ¿Cómo trabajar dentro de una rama aislada?

Dentro de la rama recién creada puedes realizar cambios con total libertad. En el ejemplo práctico se crea un archivo con el editor **Nano** :

bash nano testing_admin.txt

Después de guardar el archivo, el flujo habitual continúa:

- Ejecutar `git status` para verificar los cambios pendientes .
- Agregar los archivos al _staging area_ con `git add .` .
- Confirmar los cambios con `git commit -m "nuevo archivo creado"` .

Lo fundamental aquí es que estos cambios **solo existen en la rama admin**, no en main. Nadie más puede ver lo que acabas de hacer hasta que decidas fusionar .

## ¿Qué es fusionar ramas con git merge?

Cuando todos los cambios están listos en tu rama individual, es momento de **fusionarlos con la rama principal** para que todo el equipo acceda a ellos . El proceso requiere dos pasos:

- Regresar a la rama principal con `git checkout main` o `git switch main` .
- Ejecutar `git merge admin` para unificar los cambios .

El resultado en la terminal muestra un _**fast-forward**_, que es un método de unificación donde Git simplemente avanza el puntero de main hasta el último _commit_ de la rama fusionada . En este caso se reporta un archivo cambiado y una nueva inserción.

Un dato útil: `git switch` es el comando más moderno para cambiar de ramas y cumple exactamente la misma función que `git checkout` . Puedes usar cualquiera de los dos.

## ¿Por qué eliminar una rama después de fusionarla?

Una vez que la rama cumplió su propósito y sus cambios ya viven en main, **la buena práctica es eliminarla** . El comando para hacerlo es:

bash git branch -D admin

Eliminar ramas evita acumulación innecesaria de nombres como admin, admin1, admin2, que terminan generando confusión y posibles **conflictos** . La regla es clara: una rama existe para un propósito específico y, una vez cumplido, se elimina.

Para confirmar que todo quedó integrado, puedes ejecutar `git log` y verificar que el _commit_ aparece en el historial de la rama principal .

Si ya utilizas ramas en tus proyectos o tienes alguna estrategia diferente para organizarlas, comparte tu experiencia en los comentarios.