Construir un script en Node.js que transcribe audio con la API de Whisper de OpenAI es uno de los ejercicios más realistas para dominar el módulo _File System_. Aquí aprendes a leer un archivo `.mp3`, enviarlo como `FormData` a OpenAI y guardar la transcripción en un `.txt`, todo de forma compatible con cualquier sistema operativo.

## ¿Qué necesitas antes de transcribir audio con Whisper en Node.js?

Antes de tocar código, asegúrate de tener listos los recursos básicos para que el script funcione sin fricciones.

- Una cuenta en OpenAI con tu _API key_ generada.
- Un archivo de audio en formato `.mp3` (puedes usar uno propio o el del recurso de la clase).
- Node.js instalado y un editor listo para crear `fs-openai.js`.

> **¿Para qué sirve la API key de OpenAI?** Es la credencial que autentica tus solicitudes a Whisper. Sin ella, la API rechaza la petición y no obtienes transcripción.

## ¿Por qué usar el módulo Path junto a File System?

El módulo `path` es nativo de Node.js y resuelve un problema concreto: las rutas de archivos cambian entre Windows, Linux y macOS. Si escribes la ruta a mano, tu script se rompe al cambiar de máquina.

Al combinarlo con `fs`, logras dos cosas: leer y escribir archivos con seguridad, y hacerlo de forma transversal al sistema operativo. Por eso el script empieza importando ambos módulos con `require('fs')` y `require('path')` .

## ¿Cómo se construye la función transcribeAudio paso a paso?

La función principal es asíncrona, recibe la ruta del audio y la _API key_, y encapsula toda la lógica dentro de un bloque `try/catch` para capturar errores con claridad.

## ¿Cómo validar que el archivo de audio existe?

Antes de hacer cualquier solicitud, conviene confirmar que el archivo está disponible. Para eso usas `fs.existsSync(audioFilePath)`, que devuelve `true` o `false` de forma síncrona .

Si el archivo no existe, lanzas un error con `throw new Error('El archivo de audio no existe')`. Esto evita gastar llamadas a la API en peticiones que ya sabes que van a fallar.

## ¿Cómo preparar el FormData con Blob para enviar el audio?

Whisper espera la información en formato `multipart/form-data`, así que necesitas tres pasos concretos:

1. Leer el archivo con `fs.readFileSync(audioFilePath)` y guardarlo en `audioFile`.
2. Envolver ese contenido en un `new Blob([audioFile])` para que la API lo entienda como datos binarios.
3. Crear un `new FormData()` y agregar dos campos con `append`: el `file` con el blob y la ruta, y el `model` con el valor `whisper-1`.

El `Blob` es importante porque convierte el contenido crudo del audio en un objeto que el `fetch` puede serializar dentro del _body_ de la solicitud.

## ¿Cómo hacer la solicitud fetch a la API de Whisper?

La petición usa `fetch` apuntando a `https://api.openai.com/v1/audio/transcriptions` con método `POST` . En los `headers` envías `Authorization: Bearer ${apiKey}` y en el `body` pasas el `formData` ya construido.

> **¿Qué significa Bearer en el header Authorization?** Es el esquema de autenticación que indica a la API que el valor que sigue es un token. OpenAI valida ese token contra tu cuenta antes de procesar el audio.

Después del _fetch_ validas la respuesta con `if (!response.ok)`. Si algo falló, extraes el detalle con `await response.json()` y lanzas un `new Error` que incluye `JSON.stringify(errorData)`. Así sabes si el problema fue la _API key_, el modelo o el formato del archivo.

## ¿Cómo guardar la transcripción en un archivo TXT dinámico?

Una vez que recibes la respuesta, extraes el texto con `const transcription = data.text`. Pero el siguiente reto es guardarlo con un nombre que tenga sentido y funcione en cualquier sistema.

Para eso construyes la ruta de salida combinando varios métodos del módulo `path`:

- `path.dirname(audioFilePath)` obtiene la carpeta donde vive el audio.
- `path.basename(audioFilePath, path.extname(audioFilePath))` extrae el nombre sin la extensión `.mp3`.
- `path.join(...)` une todo y le concatena `-transcription.txt`.

Esto significa que si el audio se llama `poema.mp3`, la transcripción se guarda como `poema-transcription.txt` en la misma carpeta. Si mañana cambias el nombre del audio, el archivo de salida se adapta solo.

Finalmente usas `fs.writeFileSync(outputFilePath, transcription)` para escribir el texto y un `console.log` para informar al usuario dónde quedó guardado.

## ¿Qué aprendiste sobre File System y Path en este flujo?

Este ejercicio mezcla varias habilidades clave del desarrollo con Node.js que vale la pena identificar por nombre.

- **fs.existsSync**: validación síncrona de existencia de archivos antes de operar sobre ellos.
- **fs.readFileSync**: lectura síncrona del contenido binario de un audio.
- **fs.writeFileSync**: escritura síncrona del archivo `.txt` con la transcripción.
- **Blob y FormData**: transformación de datos binarios en un payload válido para APIs `multipart/form-data`.
- **fetch con async/await**: solicitud HTTP moderna sin dependencias externas.
- **path.join, path.dirname, path.basename, path.extname**: construcción de rutas portables entre Windows, Linux y macOS.
- **try/catch con throw new Error**: manejo de errores explícito y mensajes claros para depurar.

También quedó claro el rol de `whisper-1` como modelo de transcripción de OpenAI, y cómo el header `Authorization: Bearer` autentica cada petición con tu _API key_.