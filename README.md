# Casa de Restauración — Landing Page

Landing page pública de la iglesia. Sitio estático hecho con [Astro](https://astro.build), sin backend ni base de datos. Contenido en español.

**Sitio en producción:** https://fehrmann11.github.io/iglesia-landing-page/

## Desarrollo local

Requiere Node.js ≥22.12.

```bash
npm install
npm run dev
```

Esto levanta el servidor en `http://localhost:4321/iglesia-landing-page/`.

Para correrlo en background (útil si no quieres ocupar la terminal):

```bash
npx astro dev --background
npx astro dev status   # ver si sigue corriendo
npx astro dev logs     # ver logs
npx astro dev stop     # bajarlo
```

## Editar contenido

Todo el contenido es estático — se edita directamente en el código, no hay panel de administración (por ahora, ver `docs/roadmap.md`).

| Qué cambiar | Dónde |
| --- | --- |
| Nombre, tagline, logo, foto de portada | `src/components/Hero.astro` |
| Ministerios (nombre, descripción) | `src/components/Ministries.astro` |
| Actividades del calendario | `src/components/Calendar.astro` (arreglo `events`, arriba del componente) |
| Fotos de la galería | `src/components/Gallery.astro` + agregar la imagen a `public/images/` |
| Favicon | `public/favicon.png` |

Antes de subir imágenes nuevas, optimízalas (evita que el sitio pese mucho):

```bash
sips -s format jpeg -s formatOptions 70 -Z 1200 imagen-original.png --out public/images/nombre-final.jpg
```

## Publicar cambios (deploy)

El deploy es automático: cualquier push a la rama `main` dispara un GitHub Action que compila el sitio y lo publica en GitHub Pages.

Flujo recomendado:

```bash
# 1. Trabaja en una rama nueva a partir de develop
git checkout develop
git checkout -b feat/lo-que-sea

# 2. Haz tus cambios, commitea, y mergea de vuelta a develop
git add .
git commit -m "feat: descripción del cambio"
git checkout develop
git merge --ff-only feat/lo-que-sea
git push origin develop

# 3. Cuando quieras publicar en producción, lleva develop a main
git checkout main
git merge --ff-only develop
git push origin main   # esto dispara el deploy
```

También puedes publicar vía Pull Request (`develop` → `main`) en vez del merge manual del paso 3:

```bash
gh pr create --base main --head develop --title "Release: descripción"
gh pr merge --squash
```

Para verificar que el deploy terminó bien:

```bash
gh run watch --exit-status
```

### Bajar/subir el sitio publicado

El sitio no es un servidor que se "prenda o apague" — son archivos estáticos servidos por GitHub. Si necesitas quitarlo temporalmente de circulación:

```bash
# Bajarlo (la URL empieza a devolver 404)
gh api -X DELETE repos/fehrmann11/iglesia-landing-page/pages

# Volver a publicarlo
gh api -X POST repos/fehrmann11/iglesia-landing-page/pages -f build_type=workflow
gh workflow run deploy.yml --ref main
```

## Documentación del proyecto

Este proyecto sigue Spec-Driven Development — ver `docs/specs/` para el detalle de qué se construyó y por qué, y `docs/roadmap.md` para las próximas iteraciones (carrusel, eventos, prédicas, calendario editable por terceros, donaciones).
