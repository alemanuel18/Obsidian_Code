***
Una **red en Docker** es el mecanismo que permite que los contenedores se comuniquen entre sí, con el sistema anfitrión (host) o con redes externas. Por defecto, los contenedores funcionan en una **red interna aislada**, lo que garantiza que estén separados del mundo exterior y de otros contenedores a menos que se configure explícitamente su comunicación.

Los aspectos fundamentales de las redes en Docker son:

- **Aislamiento y Agrupación:** Los contenedores pueden estar totalmente aislados unos de otros. Para que dos o más contenedores puedan interactuar (por ejemplo, una aplicación de Node.js conectándose a una base de datos MongoDB), es necesario agruparlos dentro de una **red interna común**.
- **Comunicación por Nombre:** Dentro de una misma red, los contenedores pueden comunicarse utilizando su **nombre asignado** como si fuera un nombre de dominio. Por ejemplo, si un contenedor se llama "monguito", otros contenedores en la misma red pueden localizarlo usando ese nombre en lugar de una dirección IP.
- **Múltiples Entornos:** Docker permite crear varias redes independientes (como "mi red"), lo que facilita tener diferentes entornos de desarrollo o aplicaciones ejecutándose simultáneamente en la misma máquina sin que sus contenedores interfieran entre sí.
- **Acceso desde el Host (Port Mapping):** Debido a que la red del contenedor es privada, el mundo exterior (incluyendo tu propia computadora física) no puede acceder a sus servicios directamente. Para permitir este acceso, se utiliza el **mapeo de puertos**, que vincula un puerto de la máquina física con un puerto específico dentro de la red del contenedor.
- **Automatización con Docker Compose:** Al utilizar Docker Compose, la herramienta crea automáticamente una **red por defecto** para todos los servicios definidos en el archivo `docker-compose.yml`, permitiendo que se vean entre sí inmediatamente sin configuración manual adicional.

Para gestionar estas redes, Docker ofrece comandos específicos como `docker network ls` para listar las redes existentes, `docker network create` para generar nuevas y `docker network rm` para eliminarlas.

# Comandos
![[Docker/Paginas/Comandos Basicos#Gestión de Redes]]