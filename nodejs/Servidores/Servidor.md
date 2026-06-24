Aprende a montar un servidor HTTP en Node.js que sirve un MP4 por la ruta /video, leyendo desde disco con _fs_ y resolviendo rutas con _path_, mientras envía el contenido en **chunks** mediante **streams** y **buffers**. Con encabezados correctos y registro de bytes, comprenderás el flujo completo desde el archivo hasta el navegador.

## ¿Cómo servir video con Node.js usando streams y buffers?

Para entregar un video de forma eficiente, se crea un servidor con _http_ que escucha la ruta exacta /video, obtiene metadatos del archivo con _fs.statSync_, envía _headers_ adecuados y transmite el contenido en **fragmentos**. Así se aprovecha la naturaleza no bloqueante de _Node.js_ y la memoria se usa de forma óptima.

## ¿Qué hace la ruta /video y qué headers envía?

- Resuelve la ubicación del archivo con _path.join_ y ___dirname_ hacia "video.mp4".
- Obtiene el tamaño con _fs.statSync(videoPath)_ para calcular **Content-Length**.
- Envía **Content-Type: video/mp4** y **Content-Length: stat.size** con _res.writeHead(200, { ... })_.
- Responde únicamente cuando la URL es exactamente "/video".

## ¿Cómo se leen y envían chunks con fs.createReadStream?

- Crea un flujo de lectura con _fs.createReadStream(videoPath)_.
- Registra un contador: **chunkCounter** para monitorear envíos parciales.
- En cada evento _data_, incrementa el contador y muestra _chunk.length_ en **bytes leídos y enviados**.
- Conecta lectura y respuesta con _readStream.pipe(res)_ para transmitir sin cargar todo en memoria.

## ¿Cómo manejar errores y rutas inexistentes?

- Para rutas que no sean "/video", responde con **status code 404**, _Content-Type: text/plain_ y mensaje "Not found".
- Un "invalid status code" suele indicar que faltó el código en _res.writeHead_; se corrige enviando 404 explícitamente.

```javascript
// server-video.js
const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((req, res) => {
  if (req.url === '/video') {
    const videoPath = path.join(__dirname, 'video.mp4');
    const stat = fs.statSync(videoPath);

    res.writeHead(200, {
      'Content-Type': 'video/mp4',
      'Content-Length': stat.size,
    });

    const readStream = fs.createReadStream(videoPath);
    let chunkCounter = 0;

    readStream.on('data', (chunk) => {
      chunkCounter++;
      console.log(`chunk ${chunkCounter}: ${chunk.length} bytes leídos y enviados`);
    });

    readStream.pipe(res);
  } else {
    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not found');
  }
});

server.listen(3005, () => {
  console.log('server is running on http://localhost:3005');
});
```
## ¿Qué módulos y rutas se configuran en el servidor?

Se combinan varios módulos nativos y una ruta clara para entregar el recurso. Esto consolida habilidades clave: manejo de archivos, resolución de rutas y transmisión eficiente.

- _http_: crea el servidor y maneja _request_ y _response_.
- _fs_: lee el archivo en flujo con _fs.createReadStream_ y consulta metadatos con _fs.statSync_.
- _path_: garantiza rutas portables con _path.join(__dirname, 'video.mp4')_.
- Ruta exacta "/video": única responsable de enviar el MP4.
- Archivo requerido: coloca "video.mp4" en la raíz del proyecto. Si falta, la lectura falla y la solicitud no se completa.

## ¿Cómo probar, depurar y simular la red?

Probar con distintas condiciones ayuda a observar el comportamiento real de los **streams** y los **buffers**. Además, registrar bytes por _chunk_ facilita comprender la transferencia.

- Ejecuta con _node --watch server-video.js_ para reiniciar ante cambios.
- Abre en el navegador: [http://localhost:3005/video](http://localhost:3005/video).
- Si entras a "/", verás "Not found" por el 404 configurado.
- Usa DevTools pestaña Network y simula 3G, 4G o fast 4G para ver cómo se envían los **chunks**.
- Observa en consola: "chunk N: X bytes leídos y enviados" mientras progresa la descarga.
- Ajusta la velocidad de red para notar cómo el envío se acelera o se ralentiza según el ancho de banda.