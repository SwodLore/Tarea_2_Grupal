# DEBUG_LOG.md — Galería de Proyectos Técnicos IS093A

## Equipo
| Integrante | Rol |
|---|---|
| **Champi** | Arquitecto HTML/A11y |
| **Melgarejo** | Ingeniero CSS/Render |
| **Poves** | Validador/SEO |

---

## Errores Encontrados Durante la Validación

### Error 1: Imágenes sin atributo `alt`
- **Herramienta:** WAVE / W3C Validator
- **Descripción:** Las etiquetas `<img>` de los avatares de cada integrante no tenían el atributo `alt`, lo cual es obligatorio para accesibilidad. Los lectores de pantalla no pueden describir la imagen sin este atributo.
- **Ubicación:** Líneas con `<img src="..." class="integrante-avatar" width="48" height="48">` (3 ocurrencias)
- **Resolución manual:** Se agregó `alt="Avatar de [nombre del integrante]"` a cada etiqueta `<img>`. Esto permite que los lectores de pantalla identifiquen correctamente la imagen.
- **Antes:** `<img src="..." class="integrante-avatar" width="48" height="48">`
- **Después:** `<img src="..." class="integrante-avatar" width="48" height="48" alt="Avatar de Champi">`

### Error 2: Falta de `<meta name="description">`
- **Herramienta:** Lighthouse (SEO audit)
- **Descripción:** No se incluyó la etiqueta `<meta name="description">` en el `<head>`. Lighthouse penaliza esto en la auditoría de SEO porque los motores de búsqueda no tienen un resumen del contenido de la página.
- **Ubicación:** `<head>` del documento `index.html`
- **Resolución manual:** Se añadió manualmente la meta descripción redactada por el equipo:
  `<meta name="description" content="Galería de proyectos técnicos responsiva del equipo IS093A (Champi, Melgarejo, Poves) — UNCP. HTML5 semántico, CSS Grid/Flexbox, accesibilidad WCAG 2.1.">`
- **Impacto:** La puntuación SEO de Lighthouse subió al agregar esta meta etiqueta.

### Error 3: Contraste insuficiente en etiqueta de categoría
- **Herramienta:** WAVE (contrast checker)
- **Descripción:** La etiqueta "Valores XP" usaba una combinación de color amarillo claro (#fef08a) sobre fondo amarillo pálido (#fefce8), resultando en una relación de contraste inferior a 4.5:1 (requerido por WCAG AA).
- **Ubicación:** Clase `.tag-lowcontrast` en `styles.css`
- **Resolución manual:** Se cambió el color del texto a un tono más oscuro (#92400e — ámbar oscuro) para alcanzar una relación de contraste de al menos 4.5:1 sobre el fondo claro. También se actualizó la versión dark mode.
- **Antes:** `color: #fef08a` → ratio ≈ 1.2:1 ❌
- **Después:** `color: #92400e` → ratio ≈ 7.5:1 ✅

---

## Capturas de Lighthouse — ANTES de correcciones

> ⚠️ **Insertar aquí las capturas de pantalla de Lighthouse ANTES de aplicar las correcciones.**

| Métrica | Puntuación (Antes) |
|---|---|
| Accesibilidad | ___ |
| SEO | ___ |
| Performance | ___ |

![Lighthouse ANTES](capturas/lighthouse-antes.png)

---

## Capturas de WAVE — ANTES de correcciones

> ⚠️ **Insertar aquí las capturas de pantalla de WAVE ANTES de aplicar las correcciones.**

![WAVE ANTES](capturas/wave-antes.png)

---

## Capturas de Lighthouse — DESPUÉS de correcciones

> ⚠️ **Insertar aquí las capturas de pantalla de Lighthouse DESPUÉS de aplicar las correcciones.**

| Métrica | Puntuación (Después) |
|---|---|
| Accesibilidad | ___ |
| SEO | ___ |
| Performance | ___ |

![Lighthouse DESPUÉS](capturas/lighthouse-despues.png)

---

## Capturas de WAVE — DESPUÉS de correcciones

> ⚠️ **Insertar aquí las capturas de pantalla de WAVE DESPUÉS de aplicar las correcciones.**

![WAVE DESPUÉS](capturas/wave-despues.png)

---

## Herramientas Utilizadas
- [W3C Markup Validator](https://validator.w3.org/)
- [WAVE Web Accessibility Evaluator](https://wave.webaim.org/)
- [Chrome DevTools — Lighthouse](https://developer.chrome.com/docs/lighthouse)
- [Can I Use](https://caniuse.com/)

## Tecnologías del Proyecto
- **HTML5 semántico** con ARIA attributes
- **CSS3**: Grid + Flexbox híbrido, `clamp()`, `calc()`, custom properties
- **Modo claro/oscuro**: `@media (prefers-color-scheme: dark)` con transiciones suaves
- **Sin JavaScript** — galería 100% HTML + CSS
- **Skip-link** visible al foco para accesibilidad
- **`:focus-visible`** para navegación por teclado
