***
**Docker Compose** es una herramienta fundamental para gestionar aplicaciones que requieren varios contenedores (como una aplicación web y su base de datos) porque permite **automatizar y simplificar** procesos que, de forma manual, resultarían sumamente tediosos.

Sus principales ventajas para aplicaciones multicontenedor son:

- **Gestión con un solo comando:** Permite levantar o detener todos los servicios de una aplicación compleja (múltiples contenedores) ejecutando simplemente `docker compose up` o `docker compose down`.
- **Configuración centralizada:** Todos los parámetros de la aplicación —imágenes, puertos, volúmenes, variables de entorno y dependencias entre servicios— se definen en un único archivo de texto llamado **docker-compose.yml**.
- **Redes automáticas:** Docker Compose crea automáticamente una **red interna** para los contenedores definidos en el archivo, lo que permite que se comuniquen entre sí usando sus nombres de servicio (por ejemplo, que una app se conecte a "monguito") sin que el usuario tenga que configurar redes manualmente.
- **Logs unificados:** Al ejecutar la aplicación, la herramienta muestra los **registros (logs) de todos los contenedores en una sola ventana** de la terminal, facilitando la depuración y el seguimiento de lo que ocurre en cada servicio en tiempo real.
- **Facilidad en el desarrollo y "onboarding":** Permite que un nuevo desarrollador se integre al equipo y tenga todo el entorno funcionando (con todas sus dependencias) en cuestión de minutos con un solo comando, garantizando que todos trabajen en el mismo ambiente.
- **Gestión de múltiples entornos:** Facilita la creación de configuraciones específicas para diferentes etapas, como un **ambiente de desarrollo** (usando herramientas como `nodemon` para refrescar cambios automáticamente) y un **ambiente de producción**.
- **Eficiencia en el flujo de trabajo:** Al definir "links" o dependencias, el sistema entiende qué contenedores necesitan de otros para funcionar, estructurando el orden de arranque de forma lógica.
![[Pasted image 20260222134329.png]]