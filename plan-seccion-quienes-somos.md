# Sección 9 — Institucional: instrucciones WordPress

**Stack**: Elementor Free + Astra Free.

**Estrategia CSS** (sin Custom CSS por widget, que es Pro):
- Los widgets **HTML** aceptan un `<style>` dentro de su propio contenido → usarlo para estilos locales e interacciones hover.
- Los widgets **Heading** y **Text Editor** usan el tab `Style` del widget para color/tipografía, y `Advanced → CSS Classes` (disponible en Free) + **Apariencia → Personalizar → CSS Adicional** para lo que el tab Style no cubre.
- Los estilos **compartidos entre múltiples widgets** y las **media queries** van siempre en CSS Adicional.

---

## Estructura general

La sección es un **Section** de Elementor con **2 columnas** (50/50), fondo blanco y padding `60px 24px`.

```
[Section — fondo blanco]
  [Columna izquierda]         [Columna derecha]
    Eyebrow "Quiénes somos"     Card Sede Principal (oscura)
    H2 título                   Card Sede Olivos (blanca)
    Párrafo 1                   Card Sede Haedo (blanca)
    Párrafo 2
    Widget HTML: 3 links
```

---

## Paso 1 — Crear la sección

1. Agregar un nuevo **Section** → elegir layout **2 columnas iguales**.
2. En `Layout`:
   - **Stretch Section**: ON
   - **Content Width**: Boxed, `1200px`
   - **Padding**: `60px` top/bottom, `24px` left/right
3. En `Style`:
   - **Background Color**: `#FFFFFF`
4. **Column Gap**: en el row, usar `Custom` → `64px`.
5. En `Advanced → CSS ID`: escribir `institucional` (para que el anchor `#institucional` del menú funcione y el responsive lo apunte).

---

## Paso 2 — Columna izquierda

### 2a. Eyebrow "Quiénes somos"

Widget **Heading**:
- Texto: `Quiénes somos`
- Tag: `H3` (o `P`)
- En `Style`:
  - Color: `#2a9e2a`
  - Tipografía: Lato, `12px`, weight `700`, letter spacing `2px`, Transform: Uppercase
- Margin bottom: `12px`

### 2b. Título H2

Widget **Heading**:
- Texto: `Distrito VII del Colegio de Ingenieros de la Provincia de Buenos Aires`
- Tag: `H2`
- En `Style`:
  - Color: `#0d2d5e`
  - Tipografía: Roboto Condensed — tamaño fijo por breakpoint (Elementor Free no tiene clamp):
    - Desktop: `32px`
    - Tablet: `26px`
    - Mobile: `22px`
  - Weight: `900`, line height: `1.25`
- Margin bottom: `20px`
- En `Advanced → CSS Classes`: escribir `inst-h2`

Luego en **CSS Adicional**:

```css
.inst-h2 .elementor-heading-title {
  font-family: 'Roboto Condensed', sans-serif;
}
```

### 2c. Párrafos de descripción

**Dos widgets Text Editor**, uno debajo del otro.

**Párrafo 1** — contenido:
> El Colegio de Ingenieros de la Provincia de Buenos Aires es una entidad de carácter público no estatal, creada por Ley 10.416, que tiene a su cargo el control del ejercicio profesional de la Ingeniería en la Provincia.

**Párrafo 2** — contenido:
> El Distrito VII comprende 24 partidos de la zona norte y oeste del Gran Buenos Aires, con sede principal en San Justo (La Matanza).

Para ambos, en `Style` del widget:
- Color de texto: `#6b7a99`
- Tipografía: Lato, `14px`, weight `400`, line height `1.75`
- Párrafo 1 → margin bottom `16px`; Párrafo 2 → margin bottom `28px`

### 2d. Lista de links institucionales

Widget **HTML** — pegar el siguiente bloque completo (incluye el `<style>`):

```html
<style>
.inst-links {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.inst-link {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  border: 1px solid #e8f1fc;
  border-radius: 8px;
  color: #1a2540;
  font-size: 14px;
  font-weight: 600;
  font-family: 'Lato', sans-serif;
  text-decoration: none;
  transition: background 0.2s, border-color 0.2s;
}
.inst-link:hover {
  background: #e8f1fc;
  border-color: #2563b0;
}
.inst-link svg { flex-shrink: 0; }
.inst-link .chevron { margin-left: auto; }
</style>

<div class="inst-links">
  <a href="/autoridades" class="inst-link">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#2563b0" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path><circle cx="9" cy="7" r="4"></circle><path d="M23 21v-2a4 4 0 0 0-3-3.87"></path><path d="M16 3.13a4 4 0 0 1 0 7.75"></path></svg>
    <span>Autoridades del Distrito</span>
    <svg class="chevron" xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"></polyline></svg>
  </a>
  <a href="/normativa" class="inst-link">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#2563b0" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path><polyline points="14 2 14 8 20 8"></polyline></svg>
    <span>Normativa y resoluciones</span>
    <svg class="chevron" xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"></polyline></svg>
  </a>
  <a href="/partidos" class="inst-link">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#2563b0" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
    <span>Partidos del Distrito VII</span>
    <svg class="chevron" xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"></polyline></svg>
  </a>
</div>
```

---

## Paso 3 — Columna derecha: 3 cards de sedes

### 3a. Card Sede Principal (fondo oscuro)

Widget **HTML** — bloque completo con `<style>`:

```html
<style>
.sede-principal {
  background: #0d2d5e;
  border-radius: 12px;
  padding: 28px;
  color: white;
}
.sede-label-dark {
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: #d4f0d4;
  margin-bottom: 16px;
  font-family: 'Lato', sans-serif;
}
.sede-items-dark {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.sede-item-dark {
  display: flex;
  align-items: flex-start;
  gap: 10px;
}
.sede-item-dark svg { flex-shrink: 0; margin-top: 2px; }
.sede-item-dark span {
  font-size: 14px;
  color: rgba(255,255,255,0.85);
  line-height: 1.5;
  font-family: 'Lato', sans-serif;
}
</style>

<div class="sede-principal">
  <div class="sede-label-dark">Sede Principal</div>
  <div class="sede-items-dark">
    <div class="sede-item-dark">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.6)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
      <span>Almafuerte 2868, San Justo (La Matanza)</span>
    </div>
    <div class="sede-item-dark">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.6)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12 19.79 19.79 0 0 1 1.58 3.38 2 2 0 0 1 3.55 1h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L7.91 8.73a16 16 0 0 0 6.29 6.29l.89-.89a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
      <span>(011) 4651-0064 / 4482-2231</span>
    </div>
    <div class="sede-item-dark">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.6)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path><polyline points="22,6 12,13 2,6"></polyline></svg>
      <span>info@cipba.org</span>
    </div>
    <div class="sede-item-dark">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.6)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
      <span>Lun–Vie 9:00 a 16:00 hs</span>
    </div>
  </div>
</div>
```

### 3b. Card Sede Olivos y 3c. Card Sede Haedo (fondo blanco)

Los estilos compartidos de las cards secundarias van en **CSS Adicional** (una sola vez):

```css
/* === Sección Institucional — cards sedes secundarias === */
.sede-secundaria {
  background: white;
  border: 1px solid #e8f1fc;
  border-radius: 12px;
  padding: 22px 24px;
}
.sede-label-sec {
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: #9aa5b8;
  margin-bottom: 14px;
  font-family: 'Lato', sans-serif;
}
.sede-items-sec {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.sede-item-sec {
  display: flex;
  align-items: center;
  gap: 10px;
}
.sede-item-sec span {
  font-size: 13.5px;
  color: #6b7a99;
  font-family: 'Lato', sans-serif;
}
```

Widget **HTML** para Sede Olivos:

```html
<div class="sede-secundaria">
  <div class="sede-label-sec">Sede Olivos</div>
  <div class="sede-items-sec">
    <div class="sede-item-sec">
      <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
      <span>Ricardo Gutiérrez 1834, Olivos</span>
    </div>
    <div class="sede-item-sec">
      <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
      <span>Solo correspondencia</span>
    </div>
  </div>
</div>
```

Widget **HTML** para Sede Haedo:

```html
<div class="sede-secundaria">
  <div class="sede-label-sec">Sede Haedo</div>
  <div class="sede-items-sec">
    <div class="sede-item-sec">
      <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
      <span>Valentín Gómez 577 1° Of. 1, Haedo</span>
    </div>
    <div class="sede-item-sec">
      <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12 19.79 19.79 0 0 1 1.58 3.38 2 2 0 0 1 3.55 1h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L7.91 8.73a16 16 0 0 0 6.29 6.29l.89-.89a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
      <span>(011) 5433-5344</span>
    </div>
    <div class="sede-item-sec">
      <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
      <span>Lun–Vie 8:00 a 16:00 hs</span>
    </div>
  </div>
</div>
```

Espaciado entre las 3 cards: en la columna derecha, ir a cada widget HTML → `Advanced → Margin` → bottom `16px`. Esto sí está disponible en Free.

---

## Paso 4 — CSS Adicional completo (todo junto)

En **Apariencia → Personalizar → CSS Adicional**, agregar este bloque de una sola vez:

```css
/* === Sección Institucional === */

/* H2 tipografía Roboto Condensed */
.inst-h2 .elementor-heading-title {
  font-family: 'Roboto Condensed', sans-serif;
}

/* Cards sedes secundarias (Olivos y Haedo) */
.sede-secundaria {
  background: white;
  border: 1px solid #e8f1fc;
  border-radius: 12px;
  padding: 22px 24px;
}
.sede-label-sec {
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: #9aa5b8;
  margin-bottom: 14px;
  font-family: 'Lato', sans-serif;
}
.sede-items-sec {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.sede-item-sec {
  display: flex;
  align-items: center;
  gap: 10px;
}
.sede-item-sec span {
  font-size: 13.5px;
  color: #6b7a99;
  font-family: 'Lato', sans-serif;
}

/* Responsive: apilar columnas en ≤900px */
@media (max-width: 900px) {
  #institucional .elementor-column-wrap {
    flex-direction: column;
  }
  #institucional .elementor-column {
    width: 100% !important;
  }
}
```

> **Nota responsive**: además del CSS, en Elementor ir a vista Tablet → editar la Section → en `Layout` verificar que las columnas queden en stack. El CSS anterior fuerza el comportamiento en caso de que Elementor no lo respete.

---

## Resumen de widgets y dónde va cada CSS

| Widget | CSS Adicional | `<style>` en el widget | Tab Style del widget |
|---|---|---|---|
| Heading eyebrow | — | — | Color, tipografía, spacing |
| Heading H2 | `.inst-h2` (Roboto Condensed) | — | Color, tamaño, weight |
| Text Editor ×2 | — | — | Color, tipografía, spacing |
| HTML links institucionales | — | `.inst-links`, `.inst-link`, hover | — |
| HTML Sede Principal | — | `.sede-principal`, `.sede-label-dark`, etc. | — |
| HTML Sede Olivos | `.sede-secundaria`, etc. | — | — |
| HTML Sede Haedo | reutiliza lo anterior | — | — |
| Todos los widgets | `@media` responsive | — | Margin bottom vía Advanced |

**Sin ningún widget Pro ni Custom CSS por widget.**
