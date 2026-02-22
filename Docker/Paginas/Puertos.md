***
Los contenedores en Docker funcionan en una red interna aislada.

Para que el host pueda acceder a los servicios dentro del contenedor, es necesario mapear los puertos.

Podemos mapear cuantos puertos necesite nuestra aplicación.

Brindan un punto de acceso desde el Host hacia el Contenedor.

- El puerto 8080 se enlaza al 80 (HTTP).
- El puerto 8443 se enlaza al 443 (HTTPS).

- El puerto del host debe estar libre antes de asignarlo.
- Los puertos en uso no pueden ser mapeados nuevamente.

# ¿Qué diferencia hay entre usar un puerto específico o dejar que Docker lo elija?
La diferencia principal radica en el **control y la previsibilidad** que tienes sobre cómo acceder a tus servicios desde tu máquina física (host).

Estas son las implicaciones de cada opción según las fuentes:

1. Usar un puerto específico (Mapeo manual)

Cuando utilizas el formato `-p puerto_host:puerto_contenedor` (por ejemplo, `27017:27017`), estás definiendo explícitamente qué punto de acceso de tu máquina física se conectará al contenedor.

- **Previsibilidad:** Sabes exactamente en qué dirección acceder a tu aplicación (ej. `localhost:3000`).
- **Gestión de conflictos:** Si tienes varios contenedores de la misma aplicación, puedes asignarles puertos diferentes en el host (como `3001`, `3002`, etc.) para que no choquen entre sí, aunque internamente todos usen el mismo puerto.
- **Restricción:** El puerto que elijas en tu computadora **debe estar libre** antes de asignarlo; si ya está en uso por otro proceso, Docker no podrá realizar el mapeo.

2. Dejar que Docker elija (Mapeo dinámico)

Si ejecutas un comando como `docker create -p 27017` (indicando solo el puerto del contenedor), le entregas a Docker la decisión de qué puerto asignar en el host.

- **Asignación arbitraria:** Docker elegirá un puerto libre de manera aleatoria, generalmente en rangos muy altos (por encima del **50,000**).
- **Inconveniente:** No sabrás de antemano en qué puerto quedó expuesta tu aplicación. Para averiguarlo, tendrás que ejecutar obligatoriamente el comando `docker ps` y revisar la columna de puertos para ver cuál asignó Docker.
- **Uso:** Las fuentes recomiendan **no dejar que Docker tome la decisión** por ti, ya que puede resultar engorroso tener que buscar puertos aleatorios cada vez que levantas un servicio.