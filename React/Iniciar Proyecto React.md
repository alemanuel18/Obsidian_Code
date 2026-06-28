## 🟦 Vite + React

### Con npm

```bash
// o npm create vite@latest
npm create vite@latest mi-proyecto -- --template react
cd mi-proyecto
npm install
npm run dev
```

> [!tip] TypeScript Cambiar `react` por `react-ts` en el comando para usar TypeScript:
> 
> ```bash
> npm create vite@latest mi-proyecto -- --template react-ts
> ```

### Con bun

```bash
bun create vite mi-proyecto --template react
cd mi-proyecto
bun install
bun run dev
```

> [!tip] TypeScript
> 
> ```bash
> bun create vite mi-proyecto --template react-ts
> ```

---

## 🟩 Next.js (SSR / rutas / fullstack)

### Con npm

```bash
npx create-next-app@latest mi-proyecto
```

### Con bun

```bash
bun create next-app mi-proyecto
```

---

## ⚖️ npm vs bun

|Aspecto|npm|bun|
|---|---|---|
|Velocidad instalación|Estándar|Mucho más rápido|
|Velocidad dev server|Estándar|Más rápido|
|Compatibilidad paquetes|Máxima|Muy buena, casos raros de fricción|
|Uso en equipos grandes|✅ Más "seguro"|⚠️ Verificar que todos lo usen|

> [!warning] Nota Si el proyecto se comparte con varios colaboradores (ej. equipo RetailMax), conviene fijar un solo package manager para evitar lockfiles mixtos (`package-lock.json` vs `bun.lockb`).
