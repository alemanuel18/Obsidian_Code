# ¿Cómo crear archivos y directorios con comandos básicos?

Los archivos se crean fácilmente con el comando `touch`. Por ejemplo, generamos un archivo de texto usando:

```
touch archivo.txt
```

Para crear directorios, se utiliza `mkdir`. Puedes hacerlo de manera sencilla:

```
mkdir documentos
```

Al añadir la flag `-p`, puedes crear varias subcarpetas simultáneamente:

```
mkdir -p documentos/escuela/matematicas
```

# ¿De qué forma mover o renombrar archivos y directorios fácilmente?

Mover elementos se hace con el comando `mv`. Por ejemplo, para mover la carpeta **matemáticas** fuera de **escuela**:
```
mv escuela/matematicas .
```

Para renombrar directorios o archivos también empleas `mv`. Por ejemplo, cambiar la carpeta **escuela** a **colegio**:
```
mv escuela colegio
```

# ¿Qué necesitas saber para copiar y eliminar archivos/directorios con seguridad?

Para copiar archivos utilizas el comando `cp`:
```
cp saludo.txt adios.txt
```

Cuando copias directorios completos, debes aplicar el modo recursivo con `-r`:
```
cp -r documentos documentos_respaldo
```

Para eliminar archivos, puedes usar `rm`, pero con mucho cuidado, ya que no existe papelera en la terminal:
```
rm archivo.txt
```

Eliminar directorios requiere la opción recursiva `-r` y la opción `-f` para forzar la eliminación, siendo extremadamente cuidadoso:
```
rm -rf documentos_respaldo
```

Te recomiendo siempre verificar los comandos ejecutados usando opciones menos agresivas o el modo interactivo para evitar errores críticos.