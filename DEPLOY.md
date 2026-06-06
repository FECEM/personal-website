# Deploy - Publicación en GitHub Pages

## Estado actual (Opción B — Manual)

Por ahora el sitio se despliega manualmente. El repositorio contiene el **build estático** (HTML, CSS, JS, assets) generado por Astro desde `website/`.

### Pasos para actualizar

```powershell
# 1. Construir el sitio
cd website
npm run build

# 2. Copiar el build al repositorio
xcopy /E /Y website\dist\* fecem-personal-website\

# 3. Commitear y publicar
cd fecem-personal-website
git add .
git commit -m "Actualización sitio web"
git push
```

### Configuración de GitHub Pages

- **Source:** Deploy from branch
- **Branch:** `main` → `/ (root)`

---

## Mejora futura (Opción A — GitHub Actions)

PENDIENTE: Migrar a despliegue automatizado con GitHub Actions.

### Cambios necesarios

1. Mover/copiar el source de `website/` al repositorio (incluyendo `astro.config.mjs`, `package.json`, `src/`, `public/`)
2. Agregar `site` y `base` al `astro.config.mjs`:

   ```js
   export default defineConfig({
     site: 'https://[tu-usuario].github.io',
     base: '/fecem-personal-website',
     vite: {
       plugins: [tailwindcss()]
     }
   });
   ```

3. Crear `.github/workflows/deploy.yml` con el workflow oficial de Astro para Pages
4. Cambiar GitHub Pages Source a **GitHub Actions**
5. Eliminar archivos del build manual del repositorio (todo excepto `.gitignore`, `README.md`, `DEPLOY.md`)

### Ventajas

- Build automático en cada push
- No requiere ejecutar build local ni copiar archivos
- Historial del repositorio contiene el source, no el build

---

> **Última actualización:** 2026-06-06
