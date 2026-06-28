***
## Contexto

Reescribir el historial de Git para borrar un archivo o carpeta de **todos los commits**, no solo del último.

> [!warning] Esto reescribe el historial completo Todos los hashes de commits cambian. Si alguien más tiene el repo clonado, va a tener conflictos. Hay que avisar al equipo antes de hacer `push --force`.

---

## 1. `git filter-repo` (recomendado actualmente)

Más rápida y segura que `filter-branch`. Reemplaza oficialmente a la herramienta antigua.

```bash
# Instalar (si no lo tienes)
pip install git-filter-repo

# Eliminar una carpeta de todo el historial
git filter-repo --path carpeta/a/eliminar --invert-paths

# Eliminar un archivo específico
git filter-repo --path ruta/al/archivo.txt --invert-paths
```

> [!note] Detalle importante `filter-repo` trabaja sobre un clon fresco y por defecto **elimina los remotes** configurados (por seguridad). Después hay que volver a agregarlos:

```bash
git remote add origin <url-del-repo>
git push origin --force --all
git push origin --force --tags
```

---

## 2. BFG Repo-Cleaner

Ideal para repos grandes, muy rápido.

```bash
# Descargar bfg.jar desde https://rtyley.github.io/bfg-repo-cleaner/
git clone --mirror <url-del-repo> repo-mirror.git
cd repo-mirror.git

# Eliminar carpeta
java -jar bfg.jar --delete-folders carpeta_objetivo

# Eliminar archivo
java -jar bfg.jar --delete-files archivo.txt

git reflog expire --expire=now --all
git gc --prune=now --aggressive
git push --force
```

---

## 3. `git filter-branch` (opción clásica, más lenta)

```bash
git filter-branch --force --index-filter \
  "git rm -r --cached --ignore-unmatch carpeta/a/eliminar" \
  --prune-empty --tag-name-filter cat -- --all

# Limpiar referencias antiguas
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```

---

## Checklist post-limpieza

- [ ] Avisar al equipo antes del `push --force` (deben re-clonar, no hacer `pull`)
- [ ] Hacer `push --force` de branches y tags
- [ ] Si había credenciales o datos sensibles expuestos → **rotarlas/invalidarlas**
- [ ] Si es GitHub/GitLab → contactar soporte para purgar caché de forks/PRs antiguos

> [!danger] Sobre datos sensibles Si el archivo/carpeta contenía contraseñas o claves API, estas quedaron expuestas en commits anteriores aunque ya no estén en el código actual. Limpiar el historial **no es suficiente** — hay que rotar las credenciales.

---

## Comparativa rápida

|Herramienta|Velocidad|Cuándo usar|
|---|---|---|
|`git filter-repo`|Rápida|Opción por defecto hoy en día|
|BFG Repo-Cleaner|Muy rápida|Repos grandes, muchos commits|
|`git filter-branch`|Lenta|Solo si no se puede instalar nada más|
