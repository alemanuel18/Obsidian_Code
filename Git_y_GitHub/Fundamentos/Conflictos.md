Cuando trabajamos en equipo, el manejo de conflictos de ramas en Git es esencial para evitar problemas y asegurar una integración fluida de cambios en los archivos compartidos. Aquí te mostramos cómo se genera un conflicto de ramas y la forma efectiva de resolverlo paso a paso.

## ¿Qué es un conflicto de ramas en Git?

En un entorno colaborativo, es común que varias personas realicen modificaciones en archivos compartidos. Esto puede llevar a conflictos de ramas cuando intentamos fusionar cambios y estos alteran las modificaciones previas realizadas por otro colaborador. En estos casos, se debe elegir qué cambios se mantendrán en la rama principal.

## ¿Cómo crear un conflicto de ramas para aprender a resolverlo?

Para experimentar y entender cómo resolver un conflicto, podemos crear uno intencionalmente. Aquí están los pasos básicos:

- Verifica tu rama actual con `git branch`. Si solo tienes la rama `main`, estás listo para iniciar.
- Crea un archivo, por ejemplo, `conflict.txt`, añade contenido inicial (e.g., "línea original") y realiza un commit:
    
  ![[Pasted image 20260612121451.png]]
    
- Crea una nueva rama con `git checkout -b developer` y modifica el archivo con nuevos cambios, como "cambios desde la rama dev", realiza un commit.
- Vuelve a la rama `main` con `git checkout main` y modifica el mismo archivo en esta rama, por ejemplo, añadiendo "segundo cambio desde main", y realiza otro commit.

Al regresar a `main` y realizar la fusión de `developer`, verás el conflicto.

## ¿Cómo resolver un conflicto de ramas en Git?

Cuando Git detecta un conflicto, te indicará las diferencias entre las ramas con etiquetas que facilitan la identificación de cambios:

- Abre el archivo en conflicto. Verás secciones como `<<<<< HEAD` y `>>>>>`, que marcan los cambios en `main` y en la rama que intentas fusionar (`developer`).
- Edita el archivo eliminando las líneas de marcación y decide cuáles cambios deseas conservar, combinar o incluso reescribir.
- Guarda el archivo sin las señalizaciones de conflicto y realiza un commit para registrar la resolución:
    
![[Pasted image 20260612121514.png]]

## ¿Qué hacer después de resolver un conflicto?

Una vez resuelto el conflicto y unificada la versión final en `main`, considera eliminar la rama `developer` para evitar conflictos futuros. Esto ayuda a mantener el historial de cambios limpio y reduce la posibilidad de cometer errores en el futuro.