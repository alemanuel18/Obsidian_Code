Publicar un paquete npm puede ser directo si sigues pasos claros. Aquí se muestra cómo llevar **platzi-date** desde GitHub hasta npm con **autenticación 2FA** y una **previsualización de publicación** usando el flag --wry-run, validando nombre, versión y archivos incluidos como _README_, _package.json_ y la lógica en `src`.

## ¿Cómo preparar el repositorio en GitHub para publicar un paquete npm?

Sube el código a un repositorio y enlaza tu proyecto local con **remote origin**. Antes, valida que están los mínimos: _README_, _package.json_ y `src/index`.

- Revisa el estado con **git status**.
- Agrega cambios con **git add .**.
- Crea un **initial commit** y haz **push** a `main`.
- Verifica que el repositorio muestre descripción e instrucciones de _install_.

```
# Enlazar el remoto
git remote add origin <URL-del-repositorio>

# Verificar archivos listos
git status

# Agregar y comitear
git add .
git commit -m "initial commit"

# Enviar a GitHub
git push origin main
```

## ¿Cómo autenticarse en npm con 2FA para publicar?

Necesitas iniciar sesión en npm para poder publicar. El proceso utiliza el navegador y tu **doble factor de autenticación**.

- Crea tu cuenta en npm y conéctala con GitHub si corresponde.
- Ejecuta el comando de autenticación: `npm add user`.
- Autoriza en el navegador y valida el 2FA.
- Vuelve a la terminal ya logueado para continuar.

`# Autenticación en npm desde la terminal 
`npm add user`

## ¿Cómo validar y ejecutar npm publish con previsualización?

Antes de publicar, es clave revisar qué subirá el paquete. La previsualización con `--wry-run` confirma archivos, tamaño, versión y metadatos. Si todo luce bien, procede con la publicación.

## ¿Qué verifica npm publish --wry-run antes de publicar?

La previsualización muestra los elementos que npm empaquetará.

- Nombre del paquete: **platzi-date**.
- Versión: **1.0.0**.
- Archivos incluidos: _README_, _package.json_, archivo con la lógica (`src/index`).
- Tamaño total e **integridad** con llaves generadas.
- Conteo de archivos y nombre del archivo del paquete.
- Señal útil: si olvidaste ignorar `node_modules`, aquí lo notarías.

`# Previsualizar sin publicar 
`npm publish --wry-run`

## ¿Cómo completar la publicación y verificar en npm?

Tras validar, ejecuta la publicación. Se pedirá autenticación nuevamente en el navegador con 2FA.

- Publica el paquete desde la terminal.
- Autoriza en el navegador y confirma el 2FA.
- Revisa en tu cuenta de npm: el paquete aparece con su **URL**, nombre, cómo _install_ y versión.

`# Publicar el paquete 
`npm publish`

## ¿Cuál es el siguiente reto con documentación y versiones?

Mejora la documentación y crea una nueva versión con el repositorio de GitHub enlazado.

- Redacta una guía clara de uso e instalación.
- Agrega el enlace del repositorio en la página del paquete.
- Publica una nueva versión con los ajustes.
- Comparte el enlace de tu paquete en los comentarios.