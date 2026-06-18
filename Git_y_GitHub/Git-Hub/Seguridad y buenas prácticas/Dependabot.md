Cada aplicación moderna depende de paquetes de terceros para funcionar: Flask en Python, librerías de NPM en Node o paquetes de NuGet en .NET. Esta dependencia, aunque acelera el desarrollo, abre **brechas de seguridad** cuando esos paquetes no están actualizados. Aquí es donde **Dependabot** se convierte en una herramienta esencial dentro de GitHub, capaz de detectar vulnerabilidades, contener el problema y generar soluciones automáticas mediante _pull requests_.

## ¿Por qué los paquetes desactualizados son un riesgo de seguridad?

Cuando construyes una aplicación y quieres leer un archivo JSON, conectar una API con Flask o dar formato con colores en Node, necesitas paquetes externos . Estas dependencias de terceros hacen tu trabajo más sencillo, pero si no se mantienen al día, pueden contener **vulnerabilidades conocidas** que un atacante podría explotar.

El problema crece conforme tu proyecto se hace más grande. Entre más paquetes agregas, más difícil resulta recordar cuáles necesitan actualización. Dependabot resuelve exactamente esto: **monitorea tus dependencias de forma continua** y te alerta en cuanto detecta una versión con problemas de seguridad.

## ¿Cómo se habilita Dependabot en un repositorio de GitHub?

Para activar Dependabot, puedes ir a la sección de **Settings** del repositorio o directamente desde la pestaña de **Security** . Ambas rutas llevan al mismo lugar: _Code Security and Analysis_.

Una vez ahí, los pasos son los siguientes:

- Habilitar las **alertas de Dependabot** para recibir notificaciones sobre vulnerabilidades.
- Activar las **actualizaciones de seguridad** para que Dependabot proponga correcciones automáticas.
- Habilitar las **actualizaciones de seguridad agrupadas** para organizar mejor los cambios.
- Activar **Dependabot Version Updates**, que es la funcionalidad más importante .

Al habilitar _Version Updates_, GitHub genera automáticamente un archivo `dependabot.yml` dentro de la carpeta `.github` del repositorio. Este archivo YAML define el **intervalo de verificación** que Dependabot seguirá. Por defecto viene configurado como semanal (_weekly_), pero puede cambiarse a diario (_daily_) para un monitoreo más frecuente .

## ¿Qué contiene el archivo dependabot.yml?

El archivo `dependabot.yml` es la configuración central de Dependabot. Define qué ecosistema de paquetes monitorear y con qué frecuencia revisar nuevas versiones. Se almacena junto a otros archivos de configuración del repositorio, como los _issue templates_ .

## ¿Cómo funciona Dependabot con un paquete vulnerable en la práctica?

Para demostrar el flujo completo, se agregó intencionalmente el paquete **Newtonsoft.Json en su versión 12.0.3** a un proyecto de .NET . Este paquete, probablemente el más utilizado en el ecosistema .NET, tiene su versión estable más reciente en 13.0.3. Sin embargo, la versión 12.0.3 presenta **al menos una vulnerabilidad conocida**, señalada con un signo de exclamación en NuGet.

El paquete se instaló desde la terminal con el comando:

bash dotnet add package Newtonsoft.Json --version 12.0.3

Después de hacer _commit_ y _push_ al repositorio, ocurrió un detalle importante: como el archivo `dependabot.yml` se había creado directamente en GitHub, fue necesario ejecutar un `git pull` antes del `git push` para sincronizar los cambios remotos con los locales .

## ¿Qué sucede cuando Dependabot detecta la vulnerabilidad?

En cuestión de segundos, Dependabot identificó el problema y clasificó la alerta como de **alta prioridad** . A diferencia de _Secret Scanning_, que solo notifica, Dependabot fue un paso más allá: **creó automáticamente un _pull request_** con la actualización del paquete a la versión segura.

El _pull request_ generado por Dependabot incluye:

- La **explicación del problema** y por qué es necesario actualizar.
- La **versión actual** frente a la **versión recomendada**.
- Un análisis de **compatibilidad entre versiones**, indicando las diferencias funcionales .

Al hacer _merge_ de ese _pull request_, el archivo `.csproj` del proyecto se actualizó automáticamente a la versión 13.0.1, la más estable disponible. Incluso la **rama temporal** creada por Dependabot se eliminó sola después de la fusión .

## ¿Cuál es la mayor ventaja de usar Dependabot?

La fortaleza principal de Dependabot es que **no solo identifica el problema, sino que lo contiene y propone una solución** mediante un _pull request_ listo para fusionar . Esto permite que cualquier miembro del equipo pueda revisar y aprobar la corrección sin necesidad de investigar manualmente cada paquete.

Además, Dependabot trabaja de forma continua: cada vez que se publique una nueva versión de cualquier paquete que uses, generará un _pull request_ para mantenerte siempre con las **versiones más estables y seguras**. Esto resulta especialmente valioso en proyectos grandes con decenas de dependencias, donde es fácil olvidar una actualización crítica.