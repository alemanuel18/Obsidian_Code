En cualquier sistema operativo, los archivos de texto plano son esenciales al procesar datos o descargar información específica. Para interactuar con ellos desde una terminal, existen comandos avanzados que permiten una manipulación efectiva y cómoda. A continuación, encontrarás claves prácticas para explorar y manipular archivos de texto mediante comandos como `cat`, `less`, `head`, `tail`, `nl`, `wc` y `awk`.

# ¿Cómo explorar rápidamente el contenido de archivos en terminal?

Uno de los comandos más utilizados para visualizar contenido rápidamente es **`cat`**, que muestra todo el texto dentro del archivo instantáneamente. Sin embargo, para archivos largos como los CSV, `cat` puede resultar poco práctico, ya que muestra mucha información de golpe.

Para una visualización más controlada y con la posibilidad de navegar dentro del archivo, existe el comando **`less`**, que presenta una interfaz interactiva donde:

- Puedes moverte con facilidad por el texto.
- Para salir de la visualización, solo debes presionar la tecla "q".

# ¿Qué comandos son útiles para mostrar partes específicas de un archivo?

Cuando buscas enfocarte solo en un segmento particular del archivo, son especialmente útiles los comandos:

- **`head`**: muestra las primeras líneas de tu archivo.
- **`tail`**: presenta las últimas líneas del archivo.

Ambos tienen opciones para especificar cuántas líneas deseas visualizar. Por ejemplo, con la opción `-n`:

- `head -n 20 nombre_archivo`: muestra las primeras 20 líneas.
- `tail -n 20 nombre_archivo`: presenta las últimas 20 líneas.

# ¿Cómo obtener información detallada del archivo?

Para información adicional sobre archivos de texto, puedes emplear diversos comandos:

## ¿Contar líneas y palabras fácilmente?

- **`nl`**: numera las líneas directamente desde la terminal, facilitando la identificación rápida del texto dentro de un archivo.
- **`wc` (_Word Count_)**: brinda múltiples posibilidades para obtener estadísticas textuales claves, incluyendo:
- Cantidad total de palabras (`wc archivo -w`).
- Número total de líneas (`wc archivo -l`).

# ¿Manipular archivos CSV con eficiencia?

El comando **`awk`** es una herramienta poderosa diseñada especialmente para manipular y explorar archivos CSV:

- Permite seleccionar columnas específicas con sintaxis sencilla. Por ejemplo, para imprimir la primera columna:

```
awk '{print $1}' archivo.csv
```

- Es posible imprimir múltiples columnas indicando separadores (`-F`) y columnas específicas con `$`:

```
awk -F"," '{print $1, $3}' archivo.csv
```

Los archivos CSV suelen usar comas para separar sus valores (`Comma Separated Values`), facilitando tanto su exploración como análisis.

# ¿Cómo aprovechar al máximo estos comandos?

Además de aplicar los comandos mencionados, invita la exploración adicional consultando los manuales en línea con `man`. Investigar las opciones y banderas específicas de cada comando ayudará a obtener mejores resultados al trabajar con información textual y al realizar análisis de sistemas operativos o archivos de registros (`logs`).