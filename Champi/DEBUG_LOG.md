# DEBUG_LOG.md — Metodología XP
**Asignatura:** Desarrollo de Aplicaciones Web (IS093A)  
**Guía Práctica:** Semana 02 — Parte 1  
**Tema:** HTML5 + CSS3 + Accesibilidad — Metodología XP

---

## ERROR 1 — Jerarquía de encabezados incorrecta

**Herramienta que lo detectó:** W3C Validator / WAVE  
**Descripción del error:**  
El `<h1>` estaba dentro del `<header>` como título del logo, y luego se usaba otro `<h1>` en la sección hero. Esto rompe la jerarquía semántica del documento: solo debe existir un `<h1>` por página.

**Cómo se corrigió manualmente:**  
- El `<h1>` del encabezado se mantuvo como título principal del sitio (nombre del tema).
- El título grande del hero se cambió a `<h2>` con `id="hero-titulo"`.
- Las subsecciones usan `<h2>` y sus tarjetas internas usan `<h3>`.
- Jerarquía final: `h1 → h2 → h3` sin saltos.

**Por qué ocurrió:**  
Al tener un logotipo con nombre visible y luego un banner grande, es tentador usar `<h1>` en ambos para darle peso visual. El error ocurre por confundir tamaño visual con jerarquía semántica. El tamaño se controla con CSS (`font-size`), no con el nivel del encabezado.

---

## ERROR 2 — Falta de `aria-label` en elementos interactivos y `alt` faltante

**Herramienta que lo detectó:** WAVE Accessibility Tool  
**Descripción del error:**  
Los elementos `<article>` de roles y valores no tenían descripción accesible para lectores de pantalla. El lector solo leía "artículo" sin contexto. Además, el emoji de icono dentro de `.valor-icon` era leído en voz alta como "emoji cara de manos apretadas", interrumpiendo la lectura.

**Cómo se corrigió manualmente:**  
- Se añadió `aria-label="Valor: Comunicación"` (y similares) a cada `<article>` de las secciones de valores y roles.
- Se añadió `aria-hidden="true"` a todos los `<span>` que contienen emojis decorativos (`.valor-icon`, `.logo-icon`, `.ciclo-num`), así el lector de pantalla los omite.
- El skip-link se hizo visible al recibir foco con CSS (`:focus { top: ... }`).

**Por qué ocurrió:**  
Los emojis y elementos visuales puramente decorativos no tienen equivalente textual natural. Sin `aria-hidden`, los lectores de pantalla los verbalizan, generando una experiencia confusa. Es un error muy común al usar íconos o emojis en lugar de imágenes con `alt`.

---

## ERROR 3 — `@container` sin `container-type` en el padre

**Herramienta que lo detectó:** DevTools — Consola del navegador (advertencia CSS)  
**Descripción del error:**  
Se declaró la regla `@container practica (max-width: 240px)` en el CSS, pero el elemento padre `.practica-group` no tenía declarada la propiedad `container-type`. El navegador ignoraba silenciosamente la regla sin mostrar error visible en pantalla, pero tampoco aplicaba los estilos.

**Cómo se corrigió manualmente:**  
Se añadieron las propiedades al elemento padre:
```css
.practica-group {
  container-type: inline-size;
  container-name: practica;
}
```
`container-type: inline-size` indica que el contenedor se evalúa por su ancho (eje inline).  
`container-name: practica` da nombre al contenedor para que el `@container practica` lo identifique correctamente.

**Por qué ocurrió:**  
Las Container Queries son una característica relativamente nueva (soporte desde Chrome 105, Firefox 110). A diferencia de las Media Queries que observan la ventana, las Container Queries observan el elemento padre, por eso **el padre debe declararse explícitamente como contenedor**. Omitir `container-type` es el error más frecuente al trabajar con esta feature.

**Fallback documentado:**  
Navegadores sin soporte de `@container` (Safari < 16, Chrome < 105) siguen mostrando el layout correctamente gracias a los estilos base de `flex-direction: column` y `gap` ya definidos. Se verificó compatibilidad en [Can I Use — container queries](https://caniuse.com/css-container-queries).

---

## Bitácora de uso de IA (según instrucciones de la guía)

| Consulta realizada | Uso | Acción posterior manual |
|---|---|---|
| "¿Qué es `container-type: inline-size` vs `size`?" | Explicación de diferencia | Se eligió `inline-size` manualmente al verificar que solo se necesitaba respuesta en ancho |
| "¿Por qué `aria-hidden` no debe usarse en elementos focusables?" | Concepto de accesibilidad | Se revisó cada elemento con `aria-hidden` para asegurar que ninguno sea focusable |
| "Diferencia entre `em`, `rem` y `vw` para tipografía fluida" | Explicación de unidades | Los valores de `clamp()` se calcularon y documentaron manualmente en `:root` |

> **Nota:** Todo bloque modificado con apoyo de IA lleva comentario `/* IA: [consulta] → Corrección manual: [explicación] */` en el CSS correspondiente.

---

## Checklist de validación

- [x] W3C Validator: sin errores de estructura
- [x] Jerarquía de encabezados: `h1 → h2 → h3` correcta
- [x] `aria-label` en todos los elementos de navegación e interactivos
- [x] `aria-hidden="true"` en íconos decorativos
- [x] Skip link visible al recibir foco
- [x] Contraste: colores verificados visualmente (texto claro sobre fondo oscuro)
- [x] `@container` con `container-type` declarado en el padre
- [x] Fallback documentado para navegadores sin soporte de `@container`
- [x] Media queries para móvil (≤640px), tablet (≤1024px) y muy pequeño (≤380px)
- [x] `clamp()` y `calc()` documentados en comentarios de `:root`
- [x] Modo claro/oscuro via `@media (prefers-color-scheme)`
