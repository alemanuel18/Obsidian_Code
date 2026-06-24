# 🐘 Conectar PostgreSQL (Docker) con TablePlus

> **Tags:** #database #postgresql #docker #tableplus #devtools

---

## Requisitos previos

- [x] Docker instalado y corriendo
- [x] TablePlus instalado
- [x] Archivos `Dockerfile` y `docker-compose.yml` listos

---

## 1. Estructura del docker-compose.yml

```yaml
services:
  postgres:
    build: .
    container_name: postgres
    restart: unless-stopped
    ports:
      - "54326:5432"   # puerto_local:puerto_contenedor
    volumes:
      - postgres_data:/var/lib/postgresql/data

  adminer:
    image: adminer:latest
    container_name: adminer
    restart: unless-stopped
    ports:
      - "8080:8080"
    depends_on:
      - postgres

volumes:
  postgres_data:
```

> [!info] El puerto expuesto al exterior es el **54326**, no el 5432 estándar.

---

## 2. Levantar los contenedores

```bash
docker compose up -d
```

### ⚠️ Error común: contenedor con nombre duplicado

Si aparece este error:

```
Error: The container name "/postgres" is already in use
```

Solucionarlo con:

```bash
docker rm -f postgres adminer
docker compose up -d
```

---

## 3. Conectar TablePlus

Crear una nueva conexión con estos datos:

|Campo|Valor|
|---|---|
|Type|`PostgreSQL`|
|Host|`127.0.0.1`|
|Port|`54326`|
|User|`postgres`|
|Password|`root`|
|Database|`laboratorio`|

1. Hacer clic en **Test** → debe aparecer en verde
2. Hacer clic en **Connect**

---

## 4. Seleccionar el schema correcto

> [!warning] Problema frecuente Al conectar, TablePlus muestra tablas del sistema (`information_schema`). Estas **no se deben borrar**, son internas de PostgreSQL.

**Solución:** En la barra inferior izquierda de TablePlus, cambiar el schema de `information_schema` → **`public`**

---

## 5. Crear la base de datos del laboratorio

Abrir el editor SQL en TablePlus (`Cmd+T`) y ejecutar:

```sql
CREATE DATABASE laboratorio;
```

Luego reconectar apuntando a `laboratorio` como base de datos.

---

## 6. Cargar archivos SQL

### Opción A — Desde TablePlus

1. `Cmd+T` para abrir el editor SQL
2. Pegar el contenido del archivo `.sql`
3. `Cmd+Enter` para ejecutar

### Opción B — Para archivos grandes (10,000+ inserts)

TablePlus puede colgarse con archivos grandes. Usar el psql del contenedor:

```bash
# Copiar el archivo al contenedor
docker cp /ruta/al/archivo.sql postgres:/tmp/inserts.sql

# Ejecutarlo desde dentro del contenedor
docker exec -it postgres psql -U postgres -d laboratorio -f /tmp/inserts.sql
```

---

## 7. Acceso a Adminer (alternativa web)

|Campo|Valor|
|---|---|
|URL|`http://localhost:8080`|
|Sistema|`PostgreSQL`|
|Servidor|`postgres`|
|Usuario|`postgres`|
|Contraseña|`root`|
|Base de datos|`dbms` (opcional)|

---

## 8. Comandos útiles de Docker

```bash
# Ver contenedores corriendo
docker ps

# Detener los contenedores
docker compose down

# Detener y borrar volúmenes (⚠️ borra todos los datos)
docker compose down -v

# Ver logs del contenedor postgres
docker logs postgres
```

---

## Referencias

- [[Docker Compose]]
- [[PostgreSQL - Vistas y Rendimiento]]
- [Documentación oficial de TablePlus](https://tableplus.com/blog/2018/04/getting-started-with-tableplus.html)