Domina el módulo **process** de Node.js para leer y controlar el proceso en ejecución con precisión: identifica el **pid**, el **cwd()**, la **versión de Node.js**, la plataforma y arquitectura, consulta **variables de entorno**, mide **uso de memoria**, escucha eventos como **exit** y **SIGINT**, y crea entradas interactivas con _stdin_ para comandos como “salir”.

## ¿Qué es process en Node.js y por qué importa?

El módulo **process** es global y te da acceso directo al estado y control del proceso actual. Con él obtienes información del entorno y gestionas el ciclo de vida: desde imprimir datos clave hasta finalizar el programa de forma limpia. Es la base para crear scripts confiables, seguros y observables.

## ¿Qué información del proceso puedes leer con keywords como pid, cwd y version?

Process expone propiedades frecuentes para inspección rápida. Ejemplo: imprime id de proceso, directorio actual, versión, plataforma, arquitectura y tiempo de ejecución.

```js
console.log('ID del proceso (pid):', process.pid);
console.log('Directorio actual (cwd):', process.cwd()); // recuerda ejecutarla como función.
console.log('Versión de Node.js:', process.version);
console.log('Plataforma:', process.platform); // p. ej., Darwin.
console.log('Arquitectura:', process.arch);   // p. ej., arm.
console.log('Tiempo de ejecución (s):', process.uptime());
```

- Usa process.cwd() para obtener la carpeta real, no la función sin ejecutar.
- Verás salidas como plataforma “Darwin” y arquitectura “ARM”, según tu sistema.

## ¿Cómo acceder a variables de entorno con process.env de forma segura?

Accede a valores comunes como **PATH**, **HOME** o **USERPROFILE**, y lee **NODE_ENV** si está definido. Las variables suelen estar en mayúsculas.

```js
console.log('Variables de entorno:', process.env); // inspección general.

console.log('PATH:', process.env.PATH);
console.log('Perfil de usuario (HOME/USERPROFILE):', process.env.HOME || process.env.USERPROFILE);
console.log('NODE_ENV:', process.env.NODE_ENV ?? 'no definido');
```

- Ideal para configurar credenciales y rutas sin exponerlas en el código.
- Si una variable no existe, retorna undefined: maneja un valor por defecto.

## ¿Cómo medir el uso de memoria con memoryUsage?

Además de la configuración, process ofrece métricas de memoria del proceso actual. Útil para monitorear scripts y detectar fugas.

```js
const memory = process.memoryUsage();
console.log('Uso de memoria:', memory);
// Estructura típica:
// {
//   rss,           // resident set size.
//   heapTotal,     // heap total.
//   heapUsed,      // heap utilizado.
//   external,      // memoria externa.
//   arrayBuffers   // buffers de arrays.
// }
```

- Estas cifras vienen en bytes: queda como ejercicio convertirlas a MB para lectura más clara.
- Observa heapUsed para estimar el consumo real de la aplicación.

## ¿Cómo manejar eventos y la entrada del usuario con stdin?

Con process puedes reaccionar al fin del proceso, a señales del sistema y a lo que escriba el usuario. Esto habilita flujos interactivos limpios y controlados.

## ¿Qué eventos exit y SIGINT deberías escuchar y por qué?

Atiende el cierre natural del proceso y la interrupción con Control + C para limpiar recursos, guardar estado o registrar auditoría.

```js
process.on('exit', (code) => {
  console.log('El proceso está terminado. Código:', code);
});

process.on('SIGINT', () => { // Control + C
  console.log('Se recibió la señal de interrupción.');
  // aquí puedes limpiar tareas, cerrar conexiones, etc.
  process.exit(0);
});
```

- exit te da el código de salida: úsalo para diagnosticar.
- SIGINT permite terminar de forma controlada en una interrupción manual.

## ¿Cómo crear un eco interactivo con stdin y un comando “salir”?

Lee lo que escribe el usuario y responde. Normaliza a minúsculas para comparaciones robustas y cierra con process.exit cuando reciba “salir”.

```js
console.log("Escribe algo y presiona Enter o Control + C para salir.");

process.stdin.on('data', (data) => {
  const input = data.toString().trim();

  if (input.toLowerCase() === 'salir') {
    console.log('Comando de salida recibido.');
    process.exit(0);
  } else {
    console.log('Escribiste:', input);
    console.log("Escribe 'salir' para terminar o escribe algo más.");
  }
});
```

- Usa _stdin_ para recibir texto del usuario en consola.
- Emplea toLowerCase para tolerar “Salir”, “SALIR” o “salir”.
- Muestra instrucciones claras: guía la interacción y evita ambigüedades.