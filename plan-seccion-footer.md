# Sección 11 — Footer: instrucciones WordPress

**Stack**: Elementor Free + Astra Free + **"Header, Footer & Blocks for Elementor"** (plugin gratuito para aplicar el footer globalmente).

**Estrategia CSS**: igual que las secciones anteriores — `<style>` dentro del widget HTML para estilos locales y hover, CSS Adicional para logo, descripción brand y responsive.

---

## Plugin necesario: "Header, Footer & Blocks for Elementor"

Para que el footer aparezca en **todas las páginas** del sitio (no solo en la home), se requiere este plugin gratuito de Brainstorm Force.

**Instalar**: Plugins → Añadir nuevo → buscar `"Header Footer & Blocks for Elementor"` → Instalar y activar.

Sin este plugin, Elementor Free no puede crear plantillas globales de footer — eso es una función exclusiva de Elementor Pro. El plugin lo habilita sin costo.

---

## Estructura general

```
[Plantilla footer — Entire Site]

  [Section 1 — grid principal]
    Background: #060f1e | Padding: 48px 24px 0
    4 columnas: 37% | 21% | 21% | 21%
    ┌─────────────────┬──────────────┬───────────────┬─────────────────┐
    │ BRAND           │ TRÁMITES     │ INSTITUCIONAL │ SERVICIOS       │
    │ Logo PNG        │ Nueva Matr.  │ Autoridades   │ Capacitación    │
    │ Descripción     │ Reinscripción│ Historia      │ Seguro Prof.    │
    │                 │ Visado Online│ Normativa     │ Beneficios      │
    │                 │ Honorarios   │ Delegaciones  │ Bolsa de Trabajo│
    │                 │ Certificados │ CAAITBA       │ Contacto        │
    └─────────────────┴──────────────┴───────────────┴─────────────────┘

  [Section 2 — barra inferior]
    Background: #060f1e | Padding: 0 24px 24px
    © 2026 CIPBA Distrito VII          Almafuerte 2868, San Justo · teléfono · email
```

---

## Paso 1 — Crear la plantilla de footer

1. Ir a **Apariencia → Header Footer & Blocks → Añadir nuevo**.
2. Tipo: **Footer**.
3. En **Display On**: seleccionar **Entire Site**.
4. Abrir con Elementor.

---

## Paso 2 — Section principal: grid de 4 columnas

1. Agregar **Section** → elegir estructura de **4 columnas**.
2. Ajustar anchos de columnas:
   - Columna 1 (Brand): **37%**
   - Columnas 2, 3 y 4: **21%** cada una
3. En `Layout`:
   - **Stretch Section**: ON
   - **Content Width**: Boxed, `1200px`
   - **Padding**: top `48px`, right `24px`, bottom `0`, left `24px`
4. En `Style` → **Background Color**: `#060f1e`
5. **Column Gap**: Custom → `40px`
6. En `Advanced → CSS Classes`: `footer-grid`

---

## Paso 3 — Columna 1: Brand

### 3a. Logo

Widget **Image**:
- Imagen: `assets/logo-cipba-vii.png`
- En `Style → Width`: `auto`; en `Style → Height`: fijar `52px` con CSS (ver abajo)
- En `Style → CSS Filters`: Brightness `0`, Contrast `100` (esto invierte parcialmente; el filtro completo se aplica por CSS)
- En `Advanced → CSS Classes`: `footer-logo`
- Margin bottom: `16px`

### 3b. Descripción

Widget **Text Editor**:
- Contenido: `Entidad pública no estatal creada por Ley 10.416. Ejercicio profesional habilitado en 24 partidos de la zona oeste y norte del Gran Buenos Aires.`
- En `Advanced → CSS Classes`: `footer-brand-text`

> Los estilos de logo y descripción van en **CSS Adicional** (ver Paso 6).

---

## Paso 4 — Columnas 2–4: links

Cada columna tiene **1 widget HTML**. El `<style>` solo va en la **primera columna** (Trámites); las siguientes reutilizan las clases ya cargadas.

### Columna 2 — Trámites (incluye el `<style>`)

```html
<style>
.footer-col-title {
  color: white;
  font-weight: 800;
  font-size: 14px;
  margin-bottom: 16px;
  letter-spacing: 0.5px;
  font-family: 'Lato', sans-serif;
}
.footer-links {
  display: flex;
  flex-direction: column;
  gap: 9px;
}
.footer-link {
  font-size: 13.5px;
  color: rgba(255,255,255,0.55);
  text-decoration: none;
  font-family: 'Lato', sans-serif;
  transition: color 0.2s;
}
.footer-link:hover {
  color: #2a9e2a;
}
</style>

<div class="footer-col-title">Trámites</div>
<div class="footer-links">
  <a href="/nueva-matricula" class="footer-link">Nueva Matrícula</a>
  <a href="/reinscripcion" class="footer-link">Reinscripción</a>
  <a href="/visado-online" class="footer-link">Visado Online</a>
  <a href="/honorarios" class="footer-link">Honorarios</a>
  <a href="/certificados" class="footer-link">Certificados</a>
</div>
```

### Columna 3 — Institucional (solo HTML, sin `<style>`)

```html
<div class="footer-col-title">Institucional</div>
<div class="footer-links">
  <a href="/autoridades" class="footer-link">Autoridades</a>
  <a href="/historia" class="footer-link">Historia</a>
  <a href="/normativa" class="footer-link">Normativa</a>
  <a href="/delegaciones" class="footer-link">Delegaciones</a>
  <a href="/caaitba" class="footer-link">CAAITBA</a>
</div>
```

### Columna 4 — Servicios (solo HTML, sin `<style>`)

```html
<div class="footer-col-title">Servicios</div>
<div class="footer-links">
  <a href="/capacitacion" class="footer-link">Capacitación</a>
  <a href="/seguro-profesional" class="footer-link">Seguro Profesional</a>
  <a href="/beneficios" class="footer-link">Beneficios</a>
  <a href="/bolsa-de-trabajo" class="footer-link">Bolsa de Trabajo</a>
  <a href="/contacto" class="footer-link">Contacto</a>
</div>
```

---

## Paso 5 — Section 2: barra inferior (copyright)

Agregar una **nueva Section** debajo de la anterior:
1. Layout: Stretch ON, Boxed 1200px, Padding `0 24px 24px`
2. Style → Background Color: `#060f1e`
3. 1 columna → agregar widget **HTML**:

```html
<style>
.footer-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
  border-top: 1px solid rgba(255,255,255,0.1);
  padding-top: 20px;
}
.footer-bar span {
  font-size: 13px;
  color: rgba(255,255,255,0.35);
  font-family: 'Lato', sans-serif;
}
</style>

<div class="footer-bar">
  <span>© 2026 CIPBA Distrito VII. Todos los derechos reservados.</span>
  <span>Almafuerte 2868, San Justo · (011) 4651-0064 · info@cipba.org</span>
</div>
```

---

## Paso 6 — CSS Adicional completo

En **Apariencia → Personalizar → CSS Adicional**:

```css
/* === Footer === */

/* Logo: forzar blanco + altura */
.footer-logo img {
  filter: brightness(0) invert(1);
  opacity: 0.9;
  height: 52px;
  width: auto;
}

/* Descripción brand */
.footer-brand-text p {
  font-size: 13.5px;
  line-height: 1.7;
  color: rgba(255,255,255,0.55);
  max-width: 280px;
  font-family: 'Lato', sans-serif;
  margin: 0;
}

/* Responsive ≤640px: Brand ocupa fila completa, links en 3 columnas */
@media (max-width: 640px) {
  .footer-grid > .elementor-container > .elementor-row > .elementor-column:first-child {
    width: 100% !important;
    margin-bottom: 24px;
  }
  .footer-grid > .elementor-container > .elementor-row > .elementor-column:not(:first-child) {
    width: 33.33% !important;
  }
}

/* Responsive ≤480px: todo en 1 columna */
@media (max-width: 480px) {
  .footer-grid .elementor-column {
    width: 100% !important;
  }
  .footer-bar {
    flex-direction: column;
    text-align: center;
  }
}
```

> **Nota**: Los selectores de responsive pueden necesitar ajuste según la versión de Elementor. Si no funcionan, usar la vista **Tablet/Mobile** del editor de Elementor para fijar anchos de columna por breakpoint directamente en la UI.

---

## Resumen de widgets y CSS

| Elemento | Widget | Dónde va el CSS |
|---|---|---|
| Logo | Image | CSS Adicional (filtro + altura) vía `.footer-logo` |
| Descripción brand | Text Editor | CSS Adicional vía `.footer-brand-text` |
| Columna Trámites | HTML | `<style>` embebido (define todas las clases de links) |
| Columna Institucional | HTML | Solo HTML (reutiliza clases) |
| Columna Servicios | HTML | Solo HTML (reutiliza clases) |
| Barra copyright | HTML | `<style>` embebido (`.footer-bar`) |

**Plugin extra**: "Header, Footer & Blocks for Elementor" (free) — imprescindible para que el footer aplique globalmente.  
**Sin widgets Pro. Sin plugins de pago.**
