Construir una **API para reservas de citas médicas** con Express y PostgreSQL te permite gestionar usuarios, horarios y conflictos de agenda en un solo flujo. Aprenderás a estructurar endpoints para pacientes y administradores, instalar PostgreSQL localmente y preparar el terreno para conectarlo con tu aplicación Node.js.

## Qué arquitectura necesita una API de reservas médicas

El proyecto se organiza alrededor de tres actores principales que conviven dentro de la misma aplicación: usuarios, administradores y el motor de reservas. Cada uno tiene responsabilidades claras y endpoints específicos.

Los usuarios pueden registrarse, autenticarse, consultar su historial y gestionar sus propias citas (crear, actualizar o cancelar). El administrador, por su parte, crea bloques de horarios, define servicios y supervisa todas las reservas del sistema .

> **¿Qué hace un manejador de conflictos en una API de citas?** Es la lógica que evita que dos usuarios reserven el mismo horario al mismo tiempo. Bloquea colisiones y garantiza que cada slot quede asignado a una sola persona.

## Qué endpoints CRUD vas a construir

La API expone operaciones básicas para mantener el ciclo de vida de cada reserva:

- Crear nuevas citas o bloques de servicio.
- Leer reservas individuales o el historial completo.
- Actualizar horarios y datos de cada cita.
- Eliminar o cancelar reservas existentes.

Esta estructura CRUD se replica para los recursos de usuarios y servicios, manteniendo coherencia en toda la aplicación.

## Por qué usar PostgreSQL como base de datos

PostgreSQL administra toda la información del flujo: registros de usuarios, citas, comunicación entre endpoints y solicitudes que llegan a la API. Es el motor relacional que vamos a usar durante el curso, específicamente la **versión 17** .

Para el desarrollo inicial trabajarás con una instalación local. Más adelante migrarás a un servicio en la nube que provea la conexión necesaria, pero las primeras pruebas y todo el desarrollo arrancan desde tu propia máquina.

## Cómo instalar PostgreSQL según tu sistema operativo

Entra al sitio oficial de PostgreSQL y elige la guía según tu sistema. En macOS, una opción común es instalarlo con _Homebrew_; en GNU/Linux y Windows encontrarás paquetes y comandos específicos para cada distribución.

Una vez instalado, valida que el servicio esté corriendo. Si usaste _Homebrew_, ejecuta:

```bash 
brew services list
```

Deberías ver la versión 17 en estado activo junto con el usuario asignado .

## Cómo configurar el usuario y la contraseña en PostgreSQL

Antes de conectar Express con la base de datos, necesitas un usuario con contraseña. Empieza confirmando que `psql` está disponible:

```bash 
psql -V
```

Luego conéctate a la base por defecto y lista los roles existentes para identificar tu superusuario:

```bash 
psql postgres
```

Cada instalación genera usuarios distintos. En el ejemplo aparece un superusuario llamado `gnx`, pero en tu máquina puede ser otro nombre .

> **¿Cómo asigno una contraseña a un usuario en PostgreSQL?** Conéctate con `psql postgres` y ejecuta `ALTER USER tu_usuario WITH PASSWORD 'tu_clave';`. PostgreSQL confirmará con un mensaje de rol aplicado.

## Qué comando usar para crear la contraseña

Dentro del prompt de `psql`, ejecuta el siguiente comando reemplazando el usuario por el tuyo:

```sql 
ALTER USER gnx WITH PASSWORD 'DB1234';
```

Esta contraseña solo sirve para entorno local. Para producción, **genera una clave robusta con un _password manager_** y nunca reutilices la misma credencial entre ambientes. Las contraseñas simples como `DB1234` se usan únicamente por practicidad en ejemplos didácticos .

> **¿Por qué no debo usar la misma contraseña en local y en producción?** Porque si tu entorno de desarrollo se filtra, el atacante tendría acceso directo a la base de datos productiva. Separar credenciales reduce el radio de impacto de cualquier fuga.

## Qué sigue después de configurar PostgreSQL

Con el servicio corriendo, el usuario configurado y la contraseña asignada, ya tienes la base lista para conectar tu aplicación Express. El siguiente paso es integrar **Prisma**, un _ODM_ que actúa como orquestador entre tu API y PostgreSQL, simplificando consultas, migraciones y modelado de datos .

Si ya completaste la instalación, cuéntame en los comentarios qué versión usaste y en qué sistema operativo trabajas.