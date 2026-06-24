La seguridad en aplicaciones modernas empieza con buenas prácticas criptográficas. Aquí verás cómo usar el módulo incorporado de _Node.js_, **crypto**, para crear un **hash SHA-256** de un texto, entender su propósito y validar resultados sin complicaciones.

## ¿Qué es el módulo crypto en node.js y para qué sirve?

El módulo **crypto** es una biblioteca nativa de _Node.js_ que ofrece **funcionalidades criptográficas esenciales**. Permite trabajar con **generación de hashes**, **cifrado de información** y **firmas digitales**, entre otras tareas. Es ideal cuando necesitas **integridad**, **autenticidad** y **seguridad** en tus aplicaciones.

- Biblioteca incorporada: no requiere instalación adicional.
- Funciones clave: hashes, cifrado y firmas digitales.
- Uso típico: verificación de integridad y protección de datos.

## ¿Cómo crear un hash SHA-256 en node.js paso a paso?

La idea central es definir un texto, aplicar el algoritmo **SHA-256** y obtener su **hash** en formato hexadecimal para imprimirlo y verificarlo.

## ¿Qué código usar para generar el hash?

A continuación, un ejemplo directo que refleja el proceso explicado: importar _crypto_, definir el texto, crear el _hash_ con _createHash('sha256')_, hacer _update_ y terminar con _digest('hex')_.

```js
const crypto = require('crypto');

const text = 'hello, crypto world';

const hash = crypto
  .createHash('sha256')
  .update(text)
  .digest('hex');

console.log('Texto original:', text);
console.log('SHA-256:', hash);
```

- Importar: `require('crypto')`.
- Definir texto: _'hello, crypto world'_.
- Crear hash: `createHash('sha256')`.
- Actualizar datos: `update(text)`.
- Salida legible: `digest('hex')`.
- Ejecutar en consola: `node archivo.js`.

## ¿Cómo verificar que el hash es correcto?

La comprobación consiste en **comparar el resultado** con una herramienta que aplique el mismo algoritmo. Copias el texto original y verificas que el **hash SHA-256** coincida. También puedes observar otros algoritmos como _MD5_, _MD2_ o _MD4_, pero recuerda que aquí el foco es **SHA-256**.

- Comparar el hash generado con una herramienta externa.
- Confirmar coincidencia del inicio y final del hash.
- Asegurar el uso del mismo algoritmo: _sha-256_.

Habilidades que practicas:

- Uso de la API de _crypto_ en _Node.js_.
- Generación de **hashes** con **SHA-256**.
- Conversión de salida a **hexadecimal** con _digest('hex')_.
- Verificación básica de integridad.

## ¿Dónde se utiliza SHA-256 y por qué es importante?

**SHA** significa Security Hash Algorithm. **SHA-256** fue desarrollado por la **NSA** y produce un **valor de 256 bits** que suele representarse como **64 caracteres hexadecimales**. Es ampliamente usado en **aplicaciones de seguridad de alto nivel**, incluyendo **blockchain**, **certificados digitales** y **sistemas de firma** modernos. Es uno de los algoritmos más difundidos y **considerados criptográficamente seguros** en la actualidad.

- Longitud del resultado: 256 bits ≈ 64 caracteres hexadecimales.
- Casos de uso: blockchain, certificados digitales y firmas.
- Ventaja clave: alta adopción y robustez criptográfica.


### Ejemplos de firmas 

https://www.onlinehashcrack.com/hash-generator.php