Aprende, paso a paso y con buenas prácticas, a crear tu primer programa en _Node.js_ que recibe argumentos por terminal, valida rangos y genera un número aleatorio. Verás cómo organizar el espacio de trabajo, iniciar _git_ y configurar _npm_ con seguridad y claridad.

## ¿Cómo preparar el entorno de Node.js y el espacio de trabajo?

Tener un entorno ordenado acelera el desarrollo. Necesitas una terminal, un editor de código y una carpeta para tus proyectos. Se recomienda crear una carpeta de trabajo (por ejemplo, dev) y clasificar proyectos: de trabajo, personales o de pruebas puntuales. Así mantienes control y contexto.

## ¿Por qué usar Git desde el inicio?

- Ejecuta git init para guardar el historial local de cambios.
- No obliga a subir a _GitHub_ o _BitBucket_.
- Ayuda a recordar qué cambió, cuándo y por qué.

## ¿Cómo organizar la carpeta del proyecto?

- Crea la carpeta del proyecto: mkdir nodejs.
- Entra en la carpeta y abre el editor: code . en _Visual Studio Code_.
- Crea la estructura base: carpeta src y archivo src/index.js.

## ¿Cómo inicializar npm y configurar el proyecto?

Inicializa el proyecto con npm init. Responde a las indicaciones para definir metadatos y el punto de entrada.

## ¿Qué datos define npm init?

- Nombre: toma el de la carpeta automáticamente.
- Versión: 1.0 por defecto.
- Descripción: “Node.js examples”.
- Punto de entrada: index.js.
- Scripts de prueba: por ahora ninguno.
- Repositorio: omite si no usarás un remoto.
- Palabras clave: opcional por ahora.
- Autor: “Óscar Barajas” con correo.
- Licencia: MIT para permitir uso, distribución y ventas.

## ¿Cómo crear un generador de números aleatorios con argumentos en Node.js?

El programa genera un número aleatorio entre 1 y 100 si no recibe argumentos. Si le pasas dos valores por terminal, usa ese rango mínimo y máximo. Incluye validaciones para evitar errores por entradas inválidas.

## ¿Cómo capturar y validar argumentos por terminal?

- Captura argumentos reales a partir de la tercera posición: process.argv.slice(2).
- Define valores por defecto: min = 1 y max = 100.
- Si hay al menos dos argumentos, conviértelos con parseInt en base 10.
- Valida que no sean NaN y que min < max.
- Si el rango no es válido, muestra un mensaje y usa los valores por defecto.

```
// src/index.js
const args = process.argv.slice(2);

let min = 1;
let max = 100;

if (args.length >= 2) {
  const parseMin = parseInt(args[0], 10);
  const parseMax = parseInt(args[1], 10);

  if (!isNaN(parseMin) && !isNaN(parseMax) && parseMin < parseMax) {
    min = parseMin;
    max = parseMax;
  } else {
    console.log('rango inválido: usando valores por defecto del 1 al 100.');
  }
}

const randomNumber = Math.floor(Math.random() * (max - min + 1)) + min;
console.log(`número aleatorio generado entre ${min} y ${max}: ${randomNumber}`);

```

## Habilidades y conceptos que aplicas:

- Uso de process.argv y slice(2) para leer argumentos reales.
- Valores por defecto y reasignación controlada con let.
- Conversión numérica con parseInt y base 10.
- Validaciones con isNaN y comparación de rangos (min < max).
- Manejo de errores de usuario con mensajes claros.

## ¿Cómo generar un número aleatorio inclusivo?

- Fórmula clave: Math.floor(Math.random() * (max - min + 1)) + min.
- Math.random genera [0, 1), sin incluir 1.
- Al multiplicar por (max - min + 1) y sumar min, aseguras incluir ambos extremos del rango.

## ¿Cómo ejecutar y depurar en la terminal?

- Ejecutar sin argumentos: node src/index.js.
- Ejecutar con rango: node src/index.js 10 50.
- Entradas inválidas (por ejemplo, “hola” 20): muestra “rango inválido” y usa 1–100.
- Si aparece un error, lee el mensaje: por ejemplo, confundir process.args con process.argv impide usar slice. Los errores señalan dónde corregir.