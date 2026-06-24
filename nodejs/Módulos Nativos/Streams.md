Trabajar con **streams en Node.js** permite procesar archivos grandes sin cargarlos completos en memoria. Con el módulo **fs**, _createReadStream_, _createWriteStream_ y eventos como _data_, _end_ y _error_, se construye un flujo eficiente para leer por _chunks_, reconstruir contenido y manejar fallos de E/S con claridad.

## ¿Qué resuelven los streams en Node.js para archivos grandes?

Los **streams** optimizan operaciones de entrada y salida al procesar datos en partes pequeñas. Son ideales para archivos extensos y transmisiones de **audio o vídeo**, evitando bloqueos de memoria y mejorando el rendimiento.

- Lectura por **fragmentos** sin cargar todo el archivo.
- Escritura continua hacia un archivo de salida.
- Manejo de **eventos** para controlar el ciclo de vida del flujo.
- Uso de **UTF-8** para interpretar texto correctamente.

En el ejemplo, se procesa un libro en texto plano (convertido a **.txt**) y se **reconstruye** en otro archivo, validando lectura, escritura y finalización del flujo.

## ¿Cómo implementar lectura y escritura con fs, utf8 y eventos?

El punto de partida es crear un archivo de trabajo (por ejemplo, streams.js) y preparar los _streams_ para entrada y salida con **fs**. La lectura se hace por _chunks_ y se escribe secuencialmente en un nuevo archivo.

## ¿Cómo configurar createReadStream y createWriteStream?

Se importa **fs**, se define el archivo de entrada (por ejemplo, js.txt) con _encoding_ **utf8** y el archivo de salida (output-js.txt):

```javascript
const fs = require('fs');

const readStream = fs.createReadStream('js.txt', {
  encoding: 'utf8'
});

const writeStream = fs.createWriteStream('output-js.txt');
```

- **fs**: acceso al sistema de archivos.
- **createReadStream**: flujo de lectura con _encoding_ utf8.
- **createWriteStream**: flujo de escritura al archivo resultante.

## ¿Cómo procesar chunks con el evento data?

Cada _chunk_ leído se registra y se escribe en el archivo de salida. Esto confirma que el flujo avanza por bloques.

```javascript
readStream.on('data', (chunk) => {
  console.log('leyendo chunk', chunk);
  writeStream.write(chunk);
});
```

- **data**: entrega cada fragmento de texto.
- **console.log**: permite observar los bloques procesados.
- **write**: envía el _chunk_ al flujo de salida.

## ¿Cómo detectar fin con end y cerrar escritura?

Al terminar la lectura, se notifica y se indica que ya no se escribirá más en el archivo de salida.

```javascript
readStream.on('end', () => {
  console.log('Terminó la lectura del archivo');
  writeStream.end();
});
```

- **end**: se dispara cuando no hay más datos.
- **writeStream.end()**: cierra el flujo de salida de forma ordenada.

## ¿Cómo manejar errores y qué efecto tiene en el archivo de salida?

Es clave capturar errores tanto de lectura como de escritura. Si falla la lectura (por ejemplo, por cambiar el nombre del archivo para simular un error), el archivo de salida puede quedar vacío porque se crea pero no recibe datos.

```javascript
readStream.on('error', (err) => {
  console.log('error de lectura del archivo', err);
});

writeStream.on('error', (err) => {
  console.log('error en escritura del archivo', err);
});
```

- Si el archivo de entrada no existe, **Node.js** reporta que no puede abrirlo.
- **createWriteStream** puede crear o limpiar el archivo de salida; si no llegan _chunks_, quedará vacío.
- Al volver al estado funcional y ejecutar de nuevo con `node streams`, los _chunks_ se escriben y el archivo resultante se completa.

Ejecución recomendada para validar el flujo:

- Limpiar consola y ejecutar `node streams`.
- Observar los **chunks** y el mensaje de **fin de lectura**.
- Verificar que no hubo **error de escritura**.
- Si se simula un fallo en lectura, revisar el mensaje de **error de lectura** y reintentar con el nombre correcto.