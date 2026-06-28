Automatizar pruebas de API con **Newman** te permite llevar tus colecciones de Postman al flujo de DevOps, ejecutar validaciones desde la terminal y garantizar que cada endpoint cumpla antes de pasar a producción. Esto es clave si construyes APIs y quieres integrar testing continuo en tu despliegue.

## ¿Cómo exporto una colección de Postman para usarla con Newman?

Dentro de Postman, abre los tres puntos de tu colección, baja al apartado de más opciones y selecciona **exportar**. Se generará un archivo JSON que se guarda en tu carpeta de descargas. Ese archivo es el que vas a mover a tu proyecto, idealmente a la raíz, para ejecutarlo después desde la terminal.

> **¿Qué es Newman?** Es una herramienta de línea de comandos de Postman que ejecuta colecciones exportadas en formato JSON, lo que permite integrar las pruebas dentro de pipelines de DevOps.

La idea es simple: tomas el archivo exportado y lo conviertes en el insumo que Newman lee para correr cada request y cada test definido.

## ¿Cómo instalo Newman y ejecuto la colección?

Primero detén cualquier proceso activo en la terminal. Luego instala el paquete de forma global:

```bash 
npm install -g newman
```

La bandera `-g` indica instalación **global**, así puedes usar el comando desde cualquier ubicación. Con Newman ya disponible, ejecuta tu colección con:

```bash 
newman run fake-api-store.postman_collection.json
```

Al correrlo, verás un informe completo en la terminal con estos elementos:

- Los requests que se intentaron ejecutar.
- Las pruebas que pasaron o fallaron.
- El detalle de cada error encontrado.
- Métricas de respuesta y tiempos.

Este reporte te ayuda a debuguear y entender exactamente dónde algo no cumple con lo esperado.

## ¿Por qué conviene correr Newman contra una API real y no un mock?

Aquí viene lo interesante: si ejecutas Newman cuando tu API aún no está construida, las pruebas van a correr sobre el mock de Postman y el resultado será limitado. En cambio, cuando ya tienes tu API funcionando el informe cambia por completo, porque las pruebas se ejecutan contra los endpoints reales y validan el comportamiento verdadero.

Para probarlo, abre otro espacio de trabajo en la terminal y levanta tu servidor:

```bash 
npm run dev
```

Con la API corriendo, vuelve a ejecutar `newman run` y notarás que el reporte refleja respuestas reales, no simuladas. Newman hace las peticiones, recibe la información y compara contra los tests que definiste en Postman.

> **¿Cuándo debo correr las pruebas con Newman?** Antes de hacer commit, antes de desplegar a producción y dentro de tu pipeline de CI/CD. Así garantizas que cada cambio cumple con los tests definidos.

## ¿Cómo se integra Newman con un flujo DevOps?

El objetivo final de exportar la colección y usar Newman es meter las pruebas dentro del proceso de despliegue. Puedes ejecutar el comando en cualquier etapa del pipeline: pre commit, pre deploy o como gate antes de mandar a producción.

### Algunos puntos clave para sacarle ventaja:

- Mantén el archivo JSON versionado en la raíz del proyecto.
- Actualiza la colección cada vez que agregues o modifiques endpoints.
- Define tests claros en Postman antes de exportar, porque Newman solo ejecuta lo que ya está escrito.
- Conecta el comando dentro de tu herramienta de CI/CD favorita.

> **¿Qué ventaja da Newman frente a probar manualmente en Postman?** Newman se ejecuta desde la terminal, lo que permite automatizarlo en pipelines y correr cientos de pruebas sin intervención humana, algo imposible con la interfaz gráfica.

En la sección de recursos encontrarás la documentación oficial de Newman y el curso de DevOps de Platzi para profundizar en cómo encadenar estas pruebas con tu sistema de despliegue continuo.