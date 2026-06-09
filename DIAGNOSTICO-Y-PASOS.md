# Beemo Learning Paths — Diagnóstico y Guía de Publicación

---

## 1. DIAGNÓSTICO — Estado original del proyecto

| # | Archivo | Estado |
|---|---------|--------|
| index.html | Funcional pero con bugs | ⚠️ |
| ruta-ia.html | Funcional, sin meta ni share | ⚠️ |
| ruta-amazon.html | Funcional, sin meta ni share | ⚠️ |
| ruta-dropshipping.html | Funcional, sin meta ni share | ⚠️ |
| ruta-marketing.html | Funcional, sin meta ni share | ⚠️ |
| ruta-finanzas.html | Funcional, sin meta ni share | ⚠️ |

---

## 2. PROBLEMAS ENCONTRADOS

### CRÍTICOS
1. **CSS duplicado ~300 líneas × 6 archivos = ~1.800 líneas de código repetido.**
   Cada página cargaba los mismos estilos inline. Cualquier cambio de color o fuente requería editar 6 archivos.

2. **`index.html` tenía DOS bloques `<style>` con `.nav` definido dos veces.**
   El segundo pisaba el primero. Esto causaba comportamiento impredecible en algunos navegadores.

### IMPORTANTES
3. **Sin meta tags Open Graph ni Twitter Card.**
   Al compartir por WhatsApp o redes sociales el link aparecía sin imagen, sin título formateado ni descripción. Visualmente pobre para un asesor enviando el link a un estudiante.

4. **Sin favicon.**
   El tab del navegador mostraba el icono genéfico en vez del branding de Beemo.

5. **Sin botones de compartir.**
   El estudiante no tenía forma fácil de reenviar su ruta a un amigo o guardar el link sin copiar la URL manualmente.

6. **Sin página 404.**
   Si el estudiante accedía a un link inválido, GitHub Pages mostraba una página genérica de error sin navegación de vuelta.

7. **Sin `CNAME`, `sitemap.xml`, ni `robots.txt`.**
   Necesarios para dominio personalizado y para que Google indexe el sitio correctamente.

### MENORES
8. **Links genéricos a beemo.tv.**
   Todos los links "Ver →" apuntan a `/explora/inteligencia-artificial` (o similar) en vez de al programa específico. Cuando tengas las URLs directas de cada curso, actualiza estos links.

9. **Sin `rel="noopener"` en links externos.**
   Pequeño riesgo de seguridad/performance. Ya corregido en los archivos nuevos.

10. **`LEEME.txt` innecesario en producción.**
    Puede eliminarse antes de subir a GitHub o mantenerse (no afecta nada).

---

## 3. ESTRUCTURA RECOMENDADA (archivos entregados)

```
Plan de estudio Beemo/
│
├── index.html              ← Portada con quiz (CORREGIDO)
├── ruta-ia.html            ← Ruta IA (CORREGIDO — modelo para las demás)
├── ruta-amazon.html        ← Pendiente de aplicar mismo patrón
├── ruta-dropshipping.html  ← Pendiente de aplicar mismo patrón
├── ruta-marketing.html     ← Pendiente de aplicar mismo patrón
├── ruta-finanzas.html      ← Pendiente de aplicar mismo patrón
│
├── _template.html          ← Plantilla para crear nuevas rutas ← NUEVO
├── 404.html                ← Página de error personalizada      ← NUEVO
├── CNAME                   ← Dominio personalizado              ← NUEVO
├── sitemap.xml             ← Para Google                        ← NUEVO
├── robots.txt              ← Para buscadores                    ← NUEVO
│
└── assets/
    ├── css/
    │   └── beemo.css       ← Hoja de estilos compartida        ← NUEVO
    └── img/
        ├── favicon.svg     ← Favicon Beemo                     ← NUEVO
        └── og-default.jpg  ← (PENDIENTE: crear imagen 1200×630)
```

---

## 4. PASOS EXACTOS PARA PUBLICAR EN GITHUB PAGES

### Paso 1 — Crear el repositorio en GitHub
1. Ve a https://github.com/new
2. Nombre del repo: `beemo-learning-paths` (o `rutas`)
3. Visibilidad: **Public** (GitHub Pages gratis requiere repo público)
4. NO marques "Initialize repository"
5. Clic en **Create repository**

### Paso 2 — Subir los archivos
**Opción A — Desde la interfaz web (más fácil):**
1. En tu repositorio recién creado, clic en **"uploading an existing file"**
2. Arrastra TODOS los archivos y carpetas del proyecto
3. Commit message: `Initial commit — Beemo Learning Paths`
4. Clic en **Commit changes**

**Opción B — Desde la terminal (si tienes Git instalado):**
```bash
cd "C:\Users\LENOVO\Documents\Plan de estudio Beemo"
git init
git add .
git commit -m "Initial commit — Beemo Learning Paths"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/beemo-learning-paths.git
git push -u origin main
```

### Paso 3 — Activar GitHub Pages
1. En tu repositorio, ve a **Settings** (pestaña de arriba)
2. En el menú izquierdo: **Pages**
3. En "Source" selecciona: **Deploy from a branch**
4. Branch: **main** / Folder: **/ (root)**
5. Clic en **Save**
6. Espera 1–2 minutos
7. GitHub te mostrará la URL: `https://TU_USUARIO.github.io/beemo-learning-paths/`

### Paso 4 — Configurar dominio personalizado (beemo.study)
1. Compra el dominio `beemo.study` en Namecheap, GoDaddy o Cloudflare
2. En tu registrador de dominio, crea estos registros DNS:
   ```
   Tipo: A     Host: @    Valor: 185.199.108.153
   Tipo: A     Host: @    Valor: 185.199.109.153
   Tipo: A     Host: @    Valor: 185.199.110.153
   Tipo: A     Host: @    Valor: 185.199.111.153
   Tipo: CNAME Host: www  Valor: TU_USUARIO.github.io
   ```
3. En GitHub Settings → Pages → Custom domain: escribe `beemo.study`
4. Marca **Enforce HTTPS**
5. El archivo `CNAME` que ya está en el proyecto hace esto automáticamente

### Paso 5 — Verificar
- Abre: `https://beemo.study/`
- Abre: `https://beemo.study/ruta-ia.html`
- Comparte el link por WhatsApp y verifica que aparece la preview con imagen

---

## 5. APLICAR LAS CORRECCIONES A LAS 4 RUTAS RESTANTES

Las correcciones de `ruta-ia.html` se deben replicar en los otros 4 archivos. El patrón es:

### En el `<head>` reemplazar el bloque `<style>` por:
```html
<link rel="stylesheet" href="assets/css/beemo.css">
```

Y agregar los meta tags (cambiando los valores según la ruta):
```html
<meta name="description" content="...">
<meta property="og:title" content="...">
<meta property="og:description" content="...">
<meta property="og:image" content="https://beemo.study/assets/img/og-[SLUG].jpg">
<!-- etc. -->
```

### En el sidebar, agregar el bloque de compartir:
Copia el bloque `<div class="scard">📲 Compartir esta ruta</div>` de `ruta-ia.html`.

### Al final antes de `</body>`, añadir la función:
```js
function shareWA() { ... }
function copyLink() { ... }
function shareTwitter() { ... }
```

---

## 6. MEJORAS PRIORITARIAS (próximas semanas)

| Prioridad | Tarea | Impacto |
|-----------|-------|---------|
| 🔴 Alta | Crear imagen OG para cada ruta (1200×630px) | WhatsApp preview visual |
| 🔴 Alta | Aplicar correcciones a ruta-amazon, dropshipping, marketing, finanzas | Consistencia |
| 🟡 Media | Actualizar links "Ver →" con URLs directas a cada programa | Conversión |
| 🟡 Media | Crear rutas nuevas usando `_template.html` | Escalabilidad |
| 🟢 Baja | Google Analytics / eventos de tracking | Métricas |
| 🟢 Baja | Búsqueda interna entre rutas | UX avanzada |

---

## 7. PRÓXIMAS TAREAS RECOMENDADAS

1. **Crear imágenes OG** (1200×630px) para cada ruta — pueden generarse con Canva o Leonardo AI con el mismo degradado del hero. Guardarlas en `assets/img/og-amazon.jpg`, `og-ia.jpg`, etc.

2. **Aplicar el patrón de `ruta-ia.html` a las otras 4 rutas.** Solo es reemplazar el `<style>` por el `<link>` al CSS compartido y agregar los meta tags.

3. **Subir a GitHub y configurar el dominio** siguiendo los pasos exactos de arriba.

4. **Crear nuevas rutas** usando `_template.html`. Duplica el archivo, renómbralo `ruta-[slug].html`, y reemplaza todos los tokens `[MAYÚSCULA]`. Agrega el link en `index.html` y en `sitemap.xml`.

5. **Automatización futura con IA**: Con la plantilla estandarizada, puedes pedirle a Claude que genere el HTML completo de una nueva ruta dándole los datos del contenido. La estructura está lista para eso.

---

*Generado para Beemo.tv | smartBeemo LLC | Junio 2025*
