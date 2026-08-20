# Secciones 3–7 de la Home: instrucciones WordPress

## Overview

Este documento cubre la implementación en WordPress (Astra Free + Elementor Free) de las secciones **propias de la Home** que todavía no tenían un plan formal:

| # | Sección | Cubierta en |
|---|---|---|
| 3 | Hero (slider) + Stats Strip | Este documento |
| 4 | Acceso Rápido / Trámites | Este documento |
| 5 | Noticias | Este documento |
| 6 | Banner Visado Online | Este documento |
| 7 | Capacitación / Próximos cursos | Este documento |
| 8 | Normativa / Resoluciones | `plan-seccion-resoluciones.md` |
| 9 | Institucional (resumen) | `plan-seccion-quienes-somos.md` |
| 10 | Contacto | `plan-seccion-contacto.md` |
| 11 | Footer (global) | `plan-seccion-footer.md` |

**Fuera de alcance de este documento**: Top Bar y Navbar (secciones 1 y 2). Ya están construidos ad-hoc en el sitio y no tienen plan formal todavía — quedan pendientes de un futuro `plan-seccion-header-navbar.md`, tal como lo define `plan-inicial.md`.

Este documento reemplaza a `wpplan-chat.md` (transcript crudo de la sesión donde se resolvió la mayoría de este contenido) como referencia de implementación — todas las decisiones de esa sesión están destiladas y organizadas acá.

**Estrategia CSS general** (misma convención que el resto del handoff): widget **HTML** con `<style>` embebido para estilos locales/hover, y **Apariencia → Personalizar → CSS Adicional** para estilos compartidos y responsive — todo compatible con Elementor Free + Astra Free (sin Custom CSS por widget, que es Pro).

**Prerrequisito**: las 5 secciones se agregan, en este orden, como Sections nuevas dentro de la página `Inicio` (template Elementor Canvas), debajo del Header global y encima de Normativa (sección 8).

---

# Sección 3 — Hero (slider) + Stats Strip: instrucciones WordPress

**Stack**: **Smart Slider 3** (free) para el hero — el widget nativo **Slides de Elementor es Pro**. El Stats Strip se construye con Elementor Free puro, sin plugin adicional.

---

## Parte A — Hero (Smart Slider 3)

### Estructura general

```
[Smart Slider 3 — id "hero-cipba"]
  Slide 1: Visado Online          (bg gradiente azul)
  Slide 2: Matrícula profesional  (bg gradiente azul oscuro)
  Slide 3: Capacitación           (bg gradiente azul medio)
  Autoplay 6000ms · Indicadores tipo pill
```

### Paso 1 — Instalar y crear el slider

1. **Plugins → Añadir nuevo** → buscar **"Smart Slider 3"** → Instalar y activar.
2. **Smart Slider 3 → Añadir nuevo** → tipo **Slider en blanco** (no usar plantillas prediseñadas) → nombre `Hero CIPBA`.
3. Configuración general del slider: `Size` → `Full Width`, altura `520px` (mínima; coincide con `minHeight: 520` del prototipo).

### Paso 2 — Crear los 3 slides

Contenido exacto de `index.html` (array `slides`):

| # | Tag (badge) | Título (H1) | Descripción | CTA primario | CTA secundario | Gradiente de fondo |
|---|---|---|---|---|---|---|
| 1 | Trámites digitales | Visado Online para Ingenieros Matriculados | Realizá el visado de tus trabajos profesionales en línea, cualquier día del año, con descuento del 20% sobre la tasa presencial. | Acceder al sistema → `#tramites` | Cómo funciona → `#tramites` | `linear-gradient(135deg, #0d2d5e 0%, #1a4a8a 60%, #2563b0 100%)` |
| 2 | Matrícula profesional | Habilitá tu ejercicio profesional en el Distrito VII | Inscribite al Colegio de Ingenieros y ejercé legalmente tu profesión en los 24 partidos del Distrito VII de la Provincia de Buenos Aires. | Solicitar matrícula → `#tramites` | Requisitos → `#tramites` | `linear-gradient(135deg, #0a2247 0%, #0d2d5e 50%, #14458a 100%)` |
| 3 | Capacitación | Cursos y formación continua para profesionales | Mantenete actualizado con nuestros cursos de posgrado, seminarios técnicos y jornadas de capacitación continua. | Ver oferta académica → `#capacitacion` | Inscribirse → `#capacitacion` | `linear-gradient(135deg, #0d2d5e 0%, #1e3c6e 60%, #1a5590 100%)` |

> ⚠️ **Bug del prototipo a corregir**: en `index.html` el botón secundario de cada slide linkea a `institucional` (sin extensión). En la implementación real debe apuntar a `institucional.html`.

Para cada slide, dentro del editor de Smart Slider 3:

1. **Background Layer**: tipo Color/Gradient → pegar el gradiente de la tabla (ángulo 135°). Opcional: agregar una capa de imagen con el patrón SVG crosshatch decorativo del prototipo (`opacity: 0.05`), exportado como PNG/SVG y puesto como overlay con blend mode o simplemente baja opacidad.
2. **Layer de contenido** (alineado a la izquierda, max-width 680px):
   - **Badge/Tag**: layer tipo "Button" o "Text" estilizado como pill — fondo `rgba(42,158,42,0.2)`, borde `1px solid rgba(42,158,42,0.4)`, border-radius `20px`, padding `5px 14px`, texto `color:#d4f0d4, font-size:13px, font-weight:600, letter-spacing:0.5px`. Agregar un punto verde de 6×6px (`background:#2a9e2a; border-radius:50%`) antes del texto.
   - **H1**: layer "Heading" — `color:white`, `font-family:'Roboto Condensed'`, `font-size: clamp(26px, 4vw, 44px)`, `font-weight:900`, `line-height:1.15`.
   - **Párrafo**: layer "Text" — `color: rgba(255,255,255,0.78)`, `font-size:17px`, `line-height:1.65`, `max-width:580px`.
   - **CTA primario**: layer "Button" — `background:#2a9e2a`, `color:white`, `padding:13px 28px`, `border-radius:6px`, `font-weight:700`, `font-size:15px`, `box-shadow: 0 4px 16px rgba(42,158,42,0.4)`; hover `background:#1f7a1f` + `transform: translateY(-2px)`. Ícono chevron-right después del texto.
   - **CTA secundario**: layer "Button" — fondo transparente, `border:1px solid rgba(255,255,255,0.4)`, `color:white`, `padding:13px 24px`, `border-radius:6px`, `font-weight:600`; hover `background: rgba(255,255,255,0.1)`.

### Paso 3 — Autoplay e indicadores

1. **Slider Settings → Autoplay**: activar, `Duration: 6000ms`, loop infinito.
2. **Controls → Bullets**: activar, posición `bottom center`.
3. Estilo de los bullets: por defecto Smart Slider usa sus propias clases (típicamente `.n2-ss-bullet`). **Verificar la clase real con DevTools una vez instalado el plugin** (no está resuelta de antemano) y sobreescribir en **CSS Adicional**:

```css
/* Ajustar el selector real tras inspeccionar el DOM de Smart Slider */
.n2-ss-bullet {
  width: 8px;
  height: 8px;
  border-radius: 4px;
  background: rgba(255,255,255,0.35);
  transition: all 0.3s;
}
.n2-ss-bullet.n2-active {
  width: 28px;
  background: #2a9e2a;
}
```

### Paso 4 — Insertar el slider en la página

1. En la página `Inicio` (Elementor), agregar una **Section** con `CSS ID: inicio`.
2. Dentro, widget **Shortcode** de Elementor con el shortcode que genera Smart Slider (`[smartslider3 slider="X"]`, visible en el listado de sliders).

---

## Parte B — Stats Strip

**Stack**: Elementor Free puro, sin plugin adicional.

### Limitaciones de Elementor Free a tener en cuenta
- **Box Shadow de Section** es Pro → el borde/sombra de la franja completa va en CSS Adicional, apuntando al CSS ID de la sección.
- No hay widget de contador animado en Free → los números van como texto estático.
- No hay divisor vertical nativo entre columnas → se simula con `border-right` vía CSS Adicional.

### Estructura general

```
[Section — CSS ID: stats-strip, fondo blanco, 4 columnas iguales]
  Columna 1: 26px/900 "+8.500" · "Matriculados activos"
  Columna 2: 26px/900 "24"     · "Partidos del Distrito VII"
  Columna 3: 26px/900 "3"      · "Sedes de atención"
  Columna 4: 26px/900 "+30"    · "Años de trayectoria"
```

### Paso 1 — Crear la sección

1. Agregar **Section** justo debajo del Hero, **4 columnas iguales**.
2. `Layout` → Content Width Boxed `1200px`, Padding `0` en todos los lados.
3. `Style` → Background Color `#ffffff`.
4. `Advanced → CSS ID`: `stats-strip`.

### Paso 2 — Contenido de cada columna

Por cada una de las 4 columnas:

1. `Advanced → Padding`: `20px` arriba/abajo, `16px` izquierda/derecha.
2. Widget **Heading** (número): tag `H3`, tipografía Roboto Condensed `26px` peso `900`, color `#0d2d5e`, alineación centro.
3. Widget **Text Editor** (label): Lato `12px` peso `400`, `letter-spacing: 0.3px`, color `#9aa5b8`, margin-top `3px`, alineación centro.

Usar el contenido de la tabla de la Parte A del Paso 2 anterior — no, corresponde a esta tabla:

| Columna | Número | Label |
|---|---|---|
| 1 | +8.500 | Matriculados activos |
| 2 | 24 | Partidos del Distrito VII |
| 3 | 3 | Sedes de atención |
| 4 | +30 | Años de trayectoria |

### Paso 3 — CSS Adicional

En **Apariencia → Personalizar → CSS Adicional**:

```css
/* === Stats Strip === */
#stats-strip {
  border-bottom: 1px solid #e8f1fc;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
}
#stats-strip .elementor-column:not(:last-child) > .elementor-element-populated {
  border-right: 1px solid #e8f1fc;
}
```

### Resumen de widgets y plugins (Sección 3)

| Elemento | Solución |
|---|---|
| Slider del hero | Smart Slider 3 (free) + widget Shortcode de Elementor |
| Bullets del slider | Ajuste vía CSS Adicional (clase real a confirmar en DevTools) |
| Stats Strip | Elementor Free puro (Heading + Text Editor) |
| Divisores/box-shadow del Stats Strip | CSS Adicional |

**Sin widgets Pro. Sin plugins de pago.**

---

# Sección 4 — Acceso Rápido / Trámites: instrucciones WordPress

**Stack**: Elementor Free puro (widget HTML). No requiere plugin adicional.

**Nota**: a diferencia de las demás secciones de este documento, esta no tenía ninguna decisión previa registrada en `wpplan-chat.md` — el diseño de implementación es nuevo, siguiendo el mismo patrón ya validado en Stats Strip y Capacitación (widget HTML + CSS embebido con prefijo `cipba-` para hover y colores dinámicos que Elementor Free no soporta nativamente en columnas).

## Estructura general

```
[Section — CSS ID: tramites, fondo #f0f2f7]
  [Header: eyebrow + H2 + link "Ver todos →"]
  [Widget HTML: grid de 6 cards]
```

## Paso 1 — Crear la sección y el header

1. Agregar **Section**, 1 columna. `Layout` → Content Width Boxed `1200px`, Padding `52px 24px`.
2. `Style` → Background Color `#f0f2f7`.
3. `Advanced → CSS ID`: `tramites`.
4. Dentro, un **Inner Section** de 2 columnas para el header (Elementor Free no maneja `justify-content: space-between` fácilmente en un solo widget):
   - Columna izquierda (~70%): Heading eyebrow `"Acceso rápido"` (Lato `12px` peso `700`, `letter-spacing:2px`, uppercase, color `#2a9e2a`, margin-bottom `8px`) + Heading H2 `"Trámites y servicios"` (Roboto Condensed `clamp(22px,3vw,30px)` peso `900`, color `#0d2d5e`).
   - Columna derecha (~30%, alineada abajo/derecha): link `"Ver todos los trámites →"`, color `#2563b0`, `14px`, peso `600`.

## Paso 2 — Widget HTML con las 6 cards

Agregar un widget **HTML** debajo del header:

```html
<style>
.tramites-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 16px;
}
.tramite-card {
  background: white;
  border-radius: 10px;
  padding: 24px 18px;
  border: 1px solid #e8f1fc;
  display: flex;
  flex-direction: column;
  gap: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.04);
  text-decoration: none;
  transition: all 0.25s;
}
.tramite-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.10);
}
.tramite-icon {
  width: 44px;
  height: 44px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.tramite-icon svg { width: 22px; height: 22px; }
.tramite-title {
  font-weight: 800;
  font-size: 14.5px;
  color: #1a2540;
  font-family: 'Lato', sans-serif;
}
.tramite-desc {
  font-size: 12.5px;
  color: #6b7a99;
  line-height: 1.5;
  font-family: 'Lato', sans-serif;
}
.tramite-link {
  margin-top: auto;
  font-size: 12.5px;
  font-weight: 700;
  display: flex;
  align-items: center;
  gap: 4px;
}

.tramite-card[data-color="matricula"]:hover      { border-color: #2563b0; }
.tramite-card[data-color="visado"]:hover          { border-color: #1a8a4a; }
.tramite-card[data-color="honorarios"]:hover      { border-color: #8a1a1a; }
.tramite-card[data-color="seguro"]:hover          { border-color: #7a1a8a; }
.tramite-card[data-color="capacitacion"]:hover    { border-color: #8a5a1a; }
.tramite-card[data-color="beneficios"]:hover      { border-color: #1a6a8a; }

.tramite-icon[data-color="matricula"]      { background: #2563b018; }
.tramite-icon[data-color="visado"]          { background: #1a8a4a18; }
.tramite-icon[data-color="honorarios"]      { background: #8a1a1a18; }
.tramite-icon[data-color="seguro"]          { background: #7a1a8a18; }
.tramite-icon[data-color="capacitacion"]    { background: #8a5a1a18; }
.tramite-icon[data-color="beneficios"]      { background: #1a6a8a18; }

.tramite-card[data-color="matricula"]   .tramite-link, .tramite-icon[data-color="matricula"] svg    { color: #2563b0; stroke: #2563b0; }
.tramite-card[data-color="visado"]      .tramite-link, .tramite-icon[data-color="visado"] svg        { color: #1a8a4a; stroke: #1a8a4a; }
.tramite-card[data-color="honorarios"]  .tramite-link, .tramite-icon[data-color="honorarios"] svg    { color: #8a1a1a; stroke: #8a1a1a; }
.tramite-card[data-color="seguro"]      .tramite-link, .tramite-icon[data-color="seguro"] svg        { color: #7a1a8a; stroke: #7a1a8a; }
.tramite-card[data-color="capacitacion"] .tramite-link, .tramite-icon[data-color="capacitacion"] svg { color: #8a5a1a; stroke: #8a5a1a; }
.tramite-card[data-color="beneficios"]  .tramite-link, .tramite-icon[data-color="beneficios"] svg    { color: #1a6a8a; stroke: #1a6a8a; }
</style>

<div class="tramites-grid">
  <a href="#tramites" class="tramite-card" data-color="matricula">
    <div class="tramite-icon" data-color="matricula"><!-- ícono award --></div>
    <div class="tramite-title">Matrícula</div>
    <div class="tramite-desc">Nueva inscripción, reinscripción y certificados</div>
    <div class="tramite-link">Acceder →</div>
  </a>
  <a href="#visado" class="tramite-card" data-color="visado">
    <div class="tramite-icon" data-color="visado"><!-- ícono file --></div>
    <div class="tramite-title">Visado Online</div>
    <div class="tramite-desc">Visá tus trabajos con 20% de descuento</div>
    <div class="tramite-link">Acceder →</div>
  </a>
  <a href="#honorarios" class="tramite-card" data-color="honorarios">
    <div class="tramite-icon" data-color="honorarios"><!-- ícono dollar-sign --></div>
    <div class="tramite-title">Honorarios</div>
    <div class="tramite-desc">Planillas y calculadora de honorarios mínimos</div>
    <div class="tramite-link">Acceder →</div>
  </a>
  <a href="#seguro" class="tramite-card" data-color="seguro">
    <div class="tramite-icon" data-color="seguro"><!-- ícono shield --></div>
    <div class="tramite-title">Seguro Profesional</div>
    <div class="tramite-desc">Póliza de responsabilidad civil para matriculados</div>
    <div class="tramite-link">Acceder →</div>
  </a>
  <a href="#capacitacion" class="tramite-card" data-color="capacitacion">
    <div class="tramite-icon" data-color="capacitacion"><!-- ícono book --></div>
    <div class="tramite-title">Capacitación</div>
    <div class="tramite-desc">Cursos, seminarios y jornadas técnicas</div>
    <div class="tramite-link">Acceder →</div>
  </a>
  <a href="#beneficios" class="tramite-card" data-color="beneficios">
    <div class="tramite-icon" data-color="beneficios"><!-- ícono users --></div>
    <div class="tramite-title">Beneficios</div>
    <div class="tramite-desc">Descuentos y convenios para matriculados</div>
    <div class="tramite-link">Acceder →</div>
  </a>
</div>
```

> Reemplazar los comentarios `<!-- ícono X -->` por los SVG inline correspondientes (set Feather Icons, mismo estilo que el resto del prototipo: `award`, `file-text`, `dollar-sign`, `shield`, `book`, `users`).

### Resumen de widgets y plugins (Sección 4)

| Elemento | Solución |
|---|---|
| Header de sección | Inner Section 2 columnas (Heading + link) |
| Grid de 6 cards | Widget HTML único con `<style>` embebido |
| Hover / color por ítem | CSS embebido en el widget (atributos `data-color`) |

**Sin widgets Pro. Sin plugins de pago.**

---

# Sección 5 — Noticias: instrucciones WordPress

**Stack**: **Essential Addons for Elementor Lite** (free, slug `essential-addons-for-elementor-lite`) → widget **Post Grid**, sobre Entradas (Posts) reales de WordPress. **Code Snippets** (ya en el stack) como fallback para el badge de post destacado.

## Estructura general

```
[Section — fondo blanco, padding 60px]
  [Inner Section 2 columnas: eyebrow+H2 | link "Archivo completo"]
  [Post Grid — 4 columnas / 2 tablet / 1 mobile]
```

## Paso 1 — Preparar los posts en WordPress

1. **Entradas → Categorías**: crear `Institucional`, `Capacitación`, `Normativa`, `Visado`.
2. **Entradas → Añadir nueva**: cargar las 4 noticias del prototipo, una categoría cada una:

| Categoría | Fecha | Título | Extracto | Destacada (fijada) |
|---|---|---|---|---|
| Institucional | 18 Abr 2026 | Asamblea General Ordinaria: convocatoria a matriculados | Se convoca a todos los matriculados del Distrito VII a la Asamblea General Ordinaria del ejercicio 2025/2026 a realizarse el próximo 15 de mayo. | ✅ Sí |
| Capacitación | 14 Abr 2026 | Nuevo curso de Integración y Automatización Profesional | Inscripciones abiertas para el módulo de Nivelación. Modalidad presencial, sede San Justo. Cupos limitados. | No |
| Normativa | 9 Abr 2026 | Actualización de honorarios mínimos – 1° trimestre 2026 | El Consejo Superior aprobó la actualización del cuadro de honorarios mínimos para el primer trimestre de 2026. | No |
| Visado | 3 Abr 2026 | Sistema de visado online: nuevas funcionalidades | Se incorporaron mejoras al sistema: adjunto de planos en formato DWG y notificaciones automáticas por e-mail. | No |

3. La noticia "destacada" se marca como **Fijada** en la portada: al editar la entrada → panel derecho → **Opciones de entrada → Fijar esta entrada en la parte superior del blog**.

## Paso 2 — Instalar Essential Addons

**Plugins → Añadir nuevo** → buscar **"Essential Addons for Elementor Lite"** → Instalar y activar.

## Paso 3 — Crear la sección en Elementor

1. **Section** con `Layout` → Content Width Boxed `1200px`, Padding `60px 24px`, fondo blanco.
2. **Inner Section** de 2 columnas para el header (mismo patrón que Trámites, ya que Elementor Free no maneja bien `justify-content: space-between` en un widget único):
   - Izquierda: Heading eyebrow `"NOVEDADES"` (Lato `12px`/`700`, uppercase, `letter-spacing:2px`, color `#2a9e2a`) + Heading H2 `"Noticias del Distrito"` (Roboto Condensed `clamp(22px,3vw,30px)`/`900`, color `#0d2d5e`).
   - Derecha (alineado abajo): link/botón `"Archivo completo →"`, color `#2563b0`.

## Paso 4 — Configurar el widget Post Grid

1. Agregar widget **EA Post Grid**.
2. `Content → Query`: Post Type `Posts`, Posts per page `4`, Order by `Date`, Order `DESC`.
3. `Content → Layout`: Grid, **4 columnas desktop / 2 tablet / 1 mobile**.
4. `Style → Card`: border-radius `10px`, border `1px solid #e8f1fc`, box-shadow `0 2px 8px rgba(0,0,0,0.04)`.
5. `Style → Category Badge`: pill, `11px`, peso `700`.
6. `Style → Title`: `15.5px`, peso `800`, color `#1a2540`.
7. `Style → Excerpt`: `13.5px`, color `#6b7a99`, line-height `1.6`.
8. `Style → Read More`: color `#2563b0`, `13px`, peso `700`.

## Paso 5 — CSS Adicional: color por categoría y hover

```css
/* === Noticias: borde superior por categoría === */
.eael-post-grid .eael-grid-post[class*="category-institucional"] .eael-grid-post-holder { border-top: 3px solid #0d2d5e; }
.eael-post-grid .eael-grid-post[class*="category-capacitacion"] .eael-grid-post-holder { border-top: 3px solid #1a8a4a; }
.eael-post-grid .eael-grid-post[class*="category-normativa"] .eael-grid-post-holder { border-top: 3px solid #8a1a1a; }
.eael-post-grid .eael-grid-post[class*="category-visado"] .eael-grid-post-holder { border-top: 3px solid #2563b0; }

/* Hover */
.eael-post-grid .eael-grid-post-holder { transition: all 0.25s; }
.eael-post-grid .eael-grid-post-holder:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 28px rgba(0,0,0,0.10);
}
```

## Paso 6 — Badge "📌 Destacado" en el post fijado

Este era el punto más delicado de la sesión previa (`wpplan-chat.md`): identificar el post fijado (sticky) y no solo el primero de la lista (frágil, depende del orden).

**Intento 1 (probar primero)**: WordPress agrega la clase `sticky` al `<article>` vía `post_class()`. Verificar en DevTools si Essential Addons la propaga al render del Post Grid; si aparece `article.sticky`, alcanza con:

```css
article.sticky .eael-grid-post-holder::before {
  content: "📌 Destacado";
  display: block;
  background: #0d2d5e;
  color: #d4f0d4;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 6px 14px;
}
```

**Intento 2 (fallback si Essential Addons no propaga la clase)**: **Code Snippets → Añadir nuevo** → tipo **JavaScript** (ejecutar "Everywhere" / frontend), que consulta la REST API por posts fijados y taggea los elementos por ID:

```js
document.addEventListener('DOMContentLoaded', function () {
  fetch('/wp-json/wp/v2/posts?sticky=true&_fields=id&per_page=100')
    .then(res => res.json())
    .then(function (posts) {
      posts.forEach(function (post) {
        var el = document.querySelector('.eael-grid-post.post-' + post.id);
        if (el) el.classList.add('is-sticky-post');
      });
    });
});
```

Con el mismo CSS del badge, pero apuntando a `.is-sticky-post`:

```css
.eael-grid-post.is-sticky-post .eael-grid-post-holder::before {
  content: "📌 Destacado";
  display: block;
  background: #0d2d5e;
  color: #d4f0d4;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 6px 14px;
}
```

### Resumen de widgets y plugins (Sección 5)

| Elemento | Solución |
|---|---|
| Listado de noticias | Essential Addons for Elementor Lite → widget Post Grid |
| Datos | Entradas (Posts) nativas de WordPress + Categorías |
| Color por categoría | CSS Adicional con selector de atributo `[class*="category-X"]` |
| Badge "Destacado" | `article.sticky` (preferido) o Code Snippets (JS) + REST API como fallback |

---

# Sección 6 — Banner Visado Online: instrucciones WordPress

**Stack**: 100% estático, **Elementor Free puro**, sin plugins adicionales.

## Estructura general

```
[Section — fondo gradiente 135deg #0d2d5e → #1a4a8a]
  [Columna izquierda 60%]        [Columna derecha 40%]
    Eyebrow + H2 + párrafo         Icon List (4 ítems) + botón CTA
```

## Paso 1 — Crear la sección

1. **Section**, `Layout` → Content Width Boxed `1200px`, Padding `52px 24px`.
2. `Style → Background`: tipo **Gradient**, Linear, ángulo `135°`, Color 1 `#0d2d5e` en `0%`, Color 2 `#1a4a8a` en `100%`.
3. `Advanced → CSS ID`: `visado`.
4. Layout de 2 columnas dentro de la Section.

## Paso 2 — Columna izquierda

1. Heading (eyebrow): `"SISTEMA ONLINE"`, tag `P`, Lato `12px`/`700`, `letter-spacing:2px`, uppercase, color `#d4f0d4`, margin-bottom `12px`.
2. Heading (H2): `"Visado de trabajos profesionales 100% online"`, Roboto Condensed `clamp(22px,3vw,34px)`/`900`, `line-height:1.2`, color `#ffffff`, margin-bottom `16px`.
3. Text Editor: `"Realizá el visado de tus trabajos desde cualquier dispositivo, las 24 horas. Con 20% de descuento en la tasa de visado respecto al trámite presencial."` — Lato `16px`/`400`, `line-height:1.65`, color `rgba(255,255,255,0.75)`.

## Paso 3 — Columna derecha: checklist + CTA

**Widget Icon List** con 4 ítems:

| Texto |
|---|
| Tasa con 20% de descuento |
| Disponible 365 días al año |
| Aprobación por visador habilitado |
| Documentación 100% digital |

Config del Icon List: ícono check circular, `Style → Icon`: color `#ffffff` sobre fondo `#2a9e2a`, tamaño `22px`, `border-radius:50%`; `Style → Text`: color `rgba(255,255,255,0.85)`, `14.5px`; `Space Between`: `14px`; `Icon Spacing`: `10px`.

**Widget Button** (CTA):
- Texto: `"Acceder al sistema"`
- Link: `https://colegioingenieros.org.ar/visado` (nueva pestaña)
- `Style`: fondo `#2a9e2a`, `border-radius:6px`, Lato `15px`/`700`, texto blanco, padding `13px 24px`, `box-shadow: 0 4px 16px rgba(42,158,42,0.4)`; hover fondo `#1f7a1f`; margin-top `8px`.

### Resumen de widgets y plugins (Sección 6)

| Elemento | Solución |
|---|---|
| Texto y título | Heading + Text Editor nativos |
| Checklist | Widget Icon List nativo |
| CTA | Widget Button nativo |
| Fondo gradiente | Background → Gradient nativo de Elementor Free |

**Sin widgets Pro. Sin plugins de pago.**

---

# Sección 7 — Capacitación / Próximos cursos: instrucciones WordPress

**Stack**: **Code Snippets** (ya en el stack) para registrar el Custom Post Type `curso` y el shortcode de salida; **ACF Free** para los campos personalizados.

> Este es el enfoque **dinámico**, al que se llegó tras iterar en la sesión previa (superó a un primer intento estático porque el layout de fila horizontal no se puede lograr bien con el widget Post Grid). Es el que debe implementarse.

## Estructura general

```
[Section — fondo #f0f2f7, padding 60px]
  [Inner Section 2 columnas: eyebrow+H2 | link "Ver toda la oferta"]
  [Widget Shortcode: [cursos_cipba] ]
     → renderiza N filas .cipba-curso-row
```

## Paso 1 — Registrar el Custom Post Type

**Code Snippets → Añadir nuevo** (tipo PHP, ejecutar "Everywhere"):

```php
add_action('init', function () {
    register_post_type('curso', [
        'labels' => [
            'name'          => 'Cursos',
            'singular_name' => 'Curso',
            'add_new_item'  => 'Agregar Curso',
            'edit_item'     => 'Editar Curso',
        ],
        'public'       => true,
        'show_in_menu' => true,
        'supports'     => ['title'],
        'menu_icon'    => 'dashicons-book',
        'has_archive'  => false,
    ]);
});
```

## Paso 2 — Campos ACF

**ACF → Grupos de campos → Añadir nuevo**, asignado a `Tipo de contenido = Curso`:

| Etiqueta | Nombre del campo | Tipo |
|---|---|---|
| Modalidad | `modalidad` | Select → opciones: `Presencial`, `Virtual` |
| Fecha | `fecha` | Text (ej. "Inicia 5 Mayo 2026") |
| Vacantes | `vacantes` | Number |
| Link inscripción | `link_inscripcion` | URL |

## Paso 3 — Cargar los cursos actuales

**Cursos → Agregar Nuevo**, uno por fila:

| Título | Modalidad | Fecha | Vacantes |
|---|---|---|---|
| Integración y Automatización Profesional | Presencial | Inicia 5 Mayo 2026 | 12 |
| BIM – Building Information Modeling Módulo 1 | Presencial | Inicia 16 Mayo 2026 | 8 |
| Honorarios Mínimos: cálculo y defensa profesional | Virtual | Inicia 22 Mayo 2026 | 25 |

> ⚠️ **Discrepancia resuelta**: el color de "vacantes" tiene fuentes contradictorias. El prototipo `index.html` usa verde (`#2a9e2a`) para todos los casos — es un bug de copy-paste del prototipo. Tanto el `README.md` (sección 7: *"Vacantes < 10: color naranja-ocre; ≥ 10: verde"*) como el shortcode PHP a continuación usan **naranja `#e67e22`** para vacantes escasas. Se toma esta última como la regla correcta — **no replicar el verde del prototipo**.

## Paso 4 — Shortcode de salida `[cursos_cipba]`

**Code Snippets → Añadir nuevo** (PHP, "Everywhere"):

```php
add_shortcode('cursos_cipba', function () {
    $cursos = new WP_Query([
        'post_type'      => 'curso',
        'posts_per_page' => -1,
        'post_status'    => 'publish',
        'orderby'        => 'menu_order date',
        'order'          => 'ASC',
    ]);

    if (!$cursos->have_posts()) {
        return '<p>No hay cursos disponibles por el momento.</p>';
    }

    ob_start();
    while ($cursos->have_posts()) {
        $cursos->the_post();

        $modalidad = get_field('modalidad');
        $fecha     = get_field('fecha');
        $vacantes  = get_field('vacantes');
        $link      = get_field('link_inscripcion');

        $badge_class    = $modalidad === 'Virtual' ? 'cipba-badge-virtual' : 'cipba-badge-presencial';
        $vacantes_color = ($vacantes && $vacantes > 0 && $vacantes < 10) ? '#e67e22' : '#1a8a4a';
        ?>
        <div class="cipba-curso-row">
            <div class="cipba-curso-left">
                <div class="cipba-curso-icon">
                    <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#2563b0" stroke-width="2">
                        <path d="M4 19.5A2.5 2.5 0 016.5 17H20" />
                        <path d="M6.5 2H20v20H6.5A2.5 2.5 0 014 19.5v-15A2.5 2.5 0 016.5 2z" />
                    </svg>
                </div>
                <div class="cipba-curso-info">
                    <div class="cipba-curso-titulo"><?php the_title(); ?></div>
                    <div class="cipba-curso-meta">
                        <?php if ($fecha): ?>
                            <span class="cipba-curso-fecha">
                                <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="#6b7a99" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2" /><path d="M16 2v4M8 2v4M3 10h18" /></svg>
                                <?php echo esc_html($fecha); ?>
                            </span>
                        <?php endif; ?>
                        <?php if ($modalidad): ?>
                            <span class="cipba-badge <?php echo esc_attr($badge_class); ?>"><?php echo esc_html($modalidad); ?></span>
                        <?php endif; ?>
                    </div>
                </div>
            </div>
            <div class="cipba-curso-right">
                <?php if ($vacantes): ?>
                    <div class="cipba-vacantes">
                        <span class="cipba-vacantes-num" style="color: <?php echo esc_attr($vacantes_color); ?>"><?php echo esc_html($vacantes); ?></span>
                        <span class="cipba-vacantes-label">vacantes</span>
                    </div>
                <?php endif; ?>
                <a class="cipba-btn-inscribirse" href="<?php echo esc_url($link ?: '#'); ?>" <?php echo $link ? 'target="_blank" rel="noopener"' : ''; ?>>Inscribirse</a>
            </div>
        </div>
        <?php
    }
    wp_reset_postdata();
    return ob_get_clean();
});
```

## Paso 5 — CSS Adicional

En **Apariencia → Personalizar → CSS Adicional**:

```css
/* === Capacitación / Cursos === */
.cipba-curso-row {
    background: #fff;
    border-radius: 10px;
    padding: 20px 24px;
    border: 1px solid #e8f1fc;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 16px;
    margin-bottom: 14px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.04);
    transition: box-shadow 0.2s;
}
.cipba-curso-row:hover { box-shadow: 0 6px 20px rgba(0,0,0,0.09); }

.cipba-curso-left { display: flex; align-items: center; gap: 16px; flex: 1; min-width: 240px; }

.cipba-curso-icon {
    width: 44px; height: 44px; border-radius: 8px;
    background: #e8f1fc; display: flex;
    align-items: center; justify-content: center; flex-shrink: 0;
}

.cipba-curso-titulo { font-weight: 800; font-size: 15px; color: #1a2540; margin-bottom: 4px; font-family: 'Lato', sans-serif; }

.cipba-curso-meta { display: flex; gap: 14px; flex-wrap: wrap; align-items: center; }

.cipba-curso-fecha { font-size: 12.5px; color: #6b7a99; display: flex; align-items: center; gap: 4px; font-family: 'Lato', sans-serif; }

.cipba-badge { font-size: 11.5px; font-weight: 700; padding: 2px 10px; border-radius: 20px; font-family: 'Lato', sans-serif; }
.cipba-badge-virtual    { background: #e8f5ee; color: #1a7a3a; }
.cipba-badge-presencial { background: #e8f1fc; color: #2563b0; }

.cipba-curso-right { display: flex; align-items: center; gap: 20px; }

.cipba-vacantes { text-align: center; }
.cipba-vacantes-num   { display: block; font-size: 20px; font-weight: 900; font-family: 'Roboto Condensed', sans-serif; }
.cipba-vacantes-label { display: block; font-size: 11px; color: #9aa5b8; font-family: 'Lato', sans-serif; }

.cipba-btn-inscribirse {
    background: #0d2d5e; color: #fff;
    padding: 10px 20px; border-radius: 6px;
    font-weight: 700; font-size: 13.5px;
    text-decoration: none; white-space: nowrap;
    transition: background 0.2s; display: inline-block;
    font-family: 'Lato', sans-serif;
}
.cipba-btn-inscribirse:hover { background: #1a4a8a; color: #fff; }
```

## Paso 6 — Sección en Elementor

1. **Section**, `Layout` → Content Width Boxed `1200px`, Padding `60px 24px`, fondo `#f0f2f7`.
2. **Inner Section** 2 columnas para el header (mismo patrón que Trámites/Noticias):
   - Izquierda: Heading eyebrow `"FORMACIÓN PROFESIONAL"` (Lato `12px`/`700`, uppercase, `letter-spacing:2px`, color `#2a9e2a`) + Heading H2 `"Próximos cursos"` (Roboto Condensed `clamp(22px,3vw,30px)`/`900`, color `#0d2d5e`).
   - Derecha: link `"Ver toda la oferta →"`, color `#2563b0`, `14px`/`600`.
3. Widget **Shortcode**: `[cursos_cipba]`.

## Paso 7 — Flujo del cliente para agregar/editar cursos

Para agregar o editar un curso: **Cursos → Agregar Nuevo** → completar título + los 4 campos ACF → **Publicar**. Aparece automáticamente en la Home, sin tocar Elementor.

### Resumen de widgets y plugins (Sección 7)

| Elemento | Solución |
|---|---|
| Datos de cursos | CPT `curso` (Code Snippets) + ACF Free |
| Renderizado | Shortcode `[cursos_cipba]` (Code Snippets, PHP) + widget Shortcode de Elementor |
| Estilos | CSS Adicional (`.cipba-curso-*`) |
| Header de sección | Inner Section nativa de Elementor |

**Sin widgets Pro. Sin plugins de pago.**
