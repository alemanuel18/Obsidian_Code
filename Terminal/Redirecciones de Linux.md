Las redirecciones del sistema son una herramienta esencial para manejar eficientemente la información que generan los comandos en la terminal de Linux. Al utilizar operadores básicos, como mayor que (>), menor que (<), doble mayor que (>>) y pipe operator (|), podemos redirigir salidas, entradas y errores hacia diferentes destinos, ampliando así las posibilidades de nuestro trabajo en terminal.

# Instalacion Previa
Debes instalar un par de comandos.

```
sudo dnf install lolcat
```

```
sudo dnf install cowsay
```

# ¿Qué es una redirección de terminal y para qué sirve?

Una redirección permite transferir la salida estándar (_standard output_) de cualquier comando hacia un archivo de texto o como entrada estándar (_standard input_) de otro comando. Esto es fundamental porque:

- Puedes almacenar resultados que normalmente aparecen en pantalla directamente en archivos.
- Facilita el envío de datos entre comandos en una cadena o flujo.

# ¿Cómo almacenar resultados de comandos en archivos?

La forma más sencilla consiste en utilizar el operador de redirección mayor que (>), como en el siguiente ejemplo:

```
echo "hola mundo" > archivo_hola.txt cat archivo_hola.txt # Resultado: hola mundo
```

Si deseas agregar contenido adicional en lugar de sobreescribir, utilizas un doble mayor que (>>):

```
echo "hola personas" >> archivo_hola.txt cat archivo_hola.txt # Resultado: hola mundo, hola personas
```

# ¿Cómo funciona la redirección de entradas y salidas entre comandos?

Es posible usar la salida de un comando como entrada directa (_standard input_) de otro utilizando el denominado pipe operator (|). Por ejemplo, los comandos `LOLCAT` o `Cowsay` usados habitualmente en ejercicios educativos, pueden recibir entradas de esta manera:

```
echo "saludo colorido" | lolcat cat archivo_hola.txt | lolcat cowsay "hola mundo" | lolcat
```

# ¿Cómo capturar errores utilizando la terminal en Linux?

Los errores que se generan al ejecutar comandos pueden ser almacenados específicamente. En Linux, el flujo de errores estándar (_standard error_) es referenciado con el número 2, y puede capturarse separadamente así:

```
ls archivo_inexistente 2> errores.log cat errores.log # Contiene el mensaje de error correspondiente
```

Si quieres concatenar varios errores dentro de un mismo archivo, la redirección se realiza con:

```
# Utilizando doble mayor que, ls archivo_inexistente 2>> errores.log
```

# ¿Cómo registrar salidas y errores simultáneamente?

Otra práctica frecuente es guardar tanto la información correcta generada como los errores en un único archivo.

```
sudo apt install vim &> instalación.log
```

Aquí, `&>` indica que se almacenarán ambas informaciones (salida y error estándar) en "instalación.log".

