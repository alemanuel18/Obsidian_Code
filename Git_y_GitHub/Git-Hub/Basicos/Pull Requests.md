Colaborar en GitHub requiere evitar modificar directamente la rama principal, lo que podría causar conflictos con el trabajo de otros compañeros. En su lugar, trabajar en ramas individuales y fusionarlas mediante _Pull Requests_ (PR) es clave para un flujo de trabajo colaborativo y seguro.

## ¿Por qué evitar cambios directos en la rama principal?

Realizar cambios directamente en la rama principal (main) puede sobrescribir el trabajo no sincronizado de otros colaboradores. Este error común se evita al:

- Crear una rama separada para cada contribuyente.
- Fusionar cambios mediante una revisión en el Pull Request, antes de unirlos a la rama principal.

## ¿Cómo funciona un Pull Request?

1. **Crear una Rama Nueva**: Al iniciar cambios, crea una rama local específica. Por ejemplo, `developer01`.
2. **Subir la Rama a GitHub**: Usa `git push -u origin <rama>` para subir tu rama.
3. **Notificar al Equipo**: Al crear un Pull Request, notificas al equipo sobre tus cambios, lo que permite una revisión colaborativa (_Code Review_).

## ¿Qué papel juega la revisión de código?

El Code Review en los Pull Requests permite:

- Evaluar y comentar los cambios antes de fusionarlos.
- Aumentar la calidad y la visibilidad de los cambios propuestos.

Aunque puede ser intimidante al principio, esta práctica asegura transparencia y mejora continua en el equipo.

## ¿Cómo se fusiona un Pull Request?

1. **Comparación y Revisión**: Una vez que el equipo revisa los cambios y los aprueba, GitHub facilita la fusión con la rama principal.
2. **Resolver Conflictos**: GitHub verifica automáticamente conflictos potenciales, mostrando una marca verde si está listo para fusionarse sin problemas.
3. **Eliminar la Rama**: Tras la fusión, se elimina la rama para mantener el repositorio ordenado y listo para nuevas tareas.