***
Es un **archivo de texto** que contiene todas las instrucciones y comandos necesarios para construir una imagen.

- Define el entorno donde vivirá la aplicación (por ejemplo, una distribución de Linux específica).
- Especifica las **dependencias, configuraciones y variables** necesarias.
- Utiliza palabras reservadas como `FROM` (para indicar la imagen base), `RUN` (para ejecutar comandos de instalación), `COPY` (para mover archivos del sistema anfitrión al contenedor) y `CMD` (para definir el comando que arranca la aplicación).
- **Cada instrucción en este archivo genera una "capa"** dentro de la imagen final.
- ![[Pasted image 20260222131651.png]]