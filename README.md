# Handoff: CIPBA Distrito VII — Home Page

## Overview
Rediseño de la home del sitio institucional del **Colegio de Ingenieros de la Provincia de Buenos Aires – Distrito VII** (cipba.org). La página presenta los servicios del colegio, trámites principales, noticias, capacitación, información institucional y formulario de contacto.

## Sobre los archivos de diseño
El archivo `index.html` es un **prototipo de alta fidelidad creado en HTML/React**. Es una referencia visual y de comportamiento — **no es código de producción para copiar directamente**. La tarea del desarrollador es recrear este diseño en WordPress usando el theme y page builder elegidos (recomendado: **Astra Pro + Elementor Pro**), respetando los tokens de diseño, layouts y comportamientos documentados aquí.

## Fidelidad
**Alta fidelidad (hifi)**: colores, tipografías, espaciados e interacciones son finales. El desarrollador debe recrear la UI pixel a pixel usando las herramientas de WordPress.

---

## Stack WordPress recomendado
| Componente | Recomendación |
|---|---|
| Theme base | **Astra** |
| Page builder | **Elementor** |
| Formularios | **WPForms** o **Elementor Forms** |
| Menú megamenú | **Astra Mega Menu** (incluido en Astra Pro) |
| Cache / Performance | **LiteSpeed Cache** o **WP Rocket** |
| SEO | **Yoast SEO** o **Rank Math** |

---

## Design Tokens

### Colores
```css
--blue-deep:   #0d2d5e;   /* Fondo navbar, secciones oscuras, títulos */
--blue-mid:    #1a4a8a;   /* Hover estados, gradientes */
--blue-light:  #2563b0;   /* Links, iconos, acentos secundarios */
--blue-pale:   #e8f1fc;   /* Fondos de cards, bordes suaves */
--green:       #2a9e2a;   /* Color acento principal (logo) */
--green-dark:  #1f7a1f;   /* Hover del verde */
--green-light: #d4f0d4;   /* Fondos tintados en verde */
--white:       #f8f9fc;   /* Fondo general de la página */
--gray-light:  #f0f2f7;   /* Secciones alternas (QuickAccess, Capacitación) */
--gray-mid:    #9aa5b8;   /* Textos secundarios, iconos */
--gray-text:   #3d4b63;   /* Texto de soporte, labels */
--text:        #1a2540;   /* Texto principal */
--footer-bg:   #060f1e;   /* Footer */
```

### Tipografía
```css
/* Fuentes: Google Fonts */
font-family: 'Lato', sans-serif;           /* Texto general */
font-family: 'Roboto Condensed', sans-serif; /* Títulos de sección, navbar brand */

/* Escala tipográfica */
--text-xs:   11px / 12px
--text-sm:   13px / 13.5px
--text-base: 14px / 15px
--text-md:   16px / 17px
--text-lg:   20px
--text-xl:   clamp(22px, 3vw, 30px)   /* Títulos de sección */
--text-hero: clamp(26px, 4vw, 44px)   /* H1 del hero */

/* Pesos */
300 — subtítulos light
400 — cuerpo de texto
700 — labels, links, CTAs secundarios
800 — títulos de cards
900 — títulos principales, stats
```

### Espaciado (secciones)
```css
--section-padding-y: 52px 24px  /* QuickAccess, VisadoBanner */
--section-padding-lg: 60px 24px /* Noticias, Capacitación, Institucional, Contacto */
--max-width: 1200px              /* Contenedor máximo centrado */
--card-radius: 10px
--btn-radius: 6px
--gap-grid: 16px / 20px
```

### Sombras
```css
--shadow-card:  0 2px 8px rgba(0,0,0,0.04);
--shadow-hover: 0 8px 24px rgba(0,0,0,0.10);
--shadow-nav:   0 2px 20px rgba(0,0,0,0.25);
```

### Border radius
```css
--radius-btn:   6px
--radius-card:  10px
--radius-badge: 20px   /* pills / tags de categoría */
--radius-icon:  8px    /* contenedores de iconos */
```

---

## Secciones de la Home

### 1. Top Bar
- Fondo: `#0d2d5e`
- Altura: ~32px, texto 13px
- Contenido izquierda: teléfono, email, horario (con íconos inline SVG)
- Contenido derecha: link WhatsApp + link "Consejo Superior" con ícono external link
- En mobile: se oculta o colapsa

### 2. Navbar (sticky)
- Altura: 64px
- Fondo inicial: `#1a4a8a` → al hacer scroll: `rgba(13,45,94,0.98)` con `backdrop-filter: blur(8px)`
- Border bottom: `3px solid #2a9e2a`
- Logo: imagen PNG (`assets/logo-cipba-vii.png`) con `filter: brightness(0) invert(1)` para versión blanca. Altura: 46px.
- Links: Roboto Condensed no, Lato 13.5px weight 600, color `rgba(255,255,255,0.88)`
- Dropdowns: fondo blanco, border top `3px solid #2a9e2a`, sombra suave
- CTA derecha: botón "Visado Online" con fondo `#2a9e2a`, border-radius 5px
- Mobile: hamburger icon, menú desplegable vertical

**Links del menú:**
- Inicio
- Matrícula (dropdown: Nueva Matrícula, Reinscripción, Baja Temporal, Certificados)
- Visado (dropdown: Visado Online, Tasas y Aranceles, Honorarios Mínimos, Visadores)
- Capacitación
- Institucional (dropdown: Autoridades, Historia, Normativa, Delegaciones)
- Noticias
- Contacto

### 3. Hero (slider de 3 slides)
- Altura mínima: 520px
- Fondo: gradiente azul (varía por slide)
- Patrón decorativo: SVG crosshatch blanco con opacity 0.05
- Rotación automática cada 6 segundos
- Indicadores de slide: pills con fondo `#2a9e2a` (activo) / `rgba(255,255,255,0.35)`
- Tag badge: fondo `rgba(42,158,42,0.2)`, borde `rgba(42,158,42,0.4)`, texto `#d4f0d4`
- H1: 44px max, weight 900, blanco
- Párrafo: 17px, `rgba(255,255,255,0.78)`
- CTA primario: fondo `#2a9e2a`, sombra verde, hover oscurece + sube 2px
- CTA secundario: borde `rgba(255,255,255,0.4)`, hover fondo `rgba(255,255,255,0.1)`

**Strip de estadísticas debajo del hero:**
- 4 columnas: +8.500 Matriculados | 24 Partidos | 3 Sedes | +30 Años
- Fondo blanco, número 26px weight 900 `#0d2d5e`, label 12px gris

### 4. Acceso Rápido / Trámites
- Fondo: `#f0f2f7`
- Grid: `repeat(auto-fill, minmax(180px, 1fr))`
- Cards blancas con borde `#e8f1fc`, border-radius 10px
- Hover: translateY(-4px), sombra, borde coloreado según ítem
- 6 ítems: Matrícula, Visado Online, Honorarios, Seguro Profesional, Capacitación, Beneficios
- Cada ítem tiene: ícono 44px container, título, descripción, link "Acceder →"

### 5. Noticias
- Fondo: blanco
- Grid: `repeat(auto-fill, minmax(280px, 1fr))`
- Border top de cards: 3px con color de categoría
- Categorías y colores:
  - Institucional: `#0d2d5e`
  - Capacitación: `#1a8a4a`
  - Normativa: `#8a1a1a`
  - Visado: `#2563b0`
- Card destacada: banner superior `#0d2d5e` con "📌 Destacado"

### 6. Banner Visado Online
- Fondo: gradiente `linear-gradient(135deg, #0d2d5e, #1a4a8a)`
- Layout: texto izquierda + checklist derecha + botón CTA
- 4 features con checkmark circular verde `#2a9e2a`
- Botón: `#2a9e2a` con sombra verde

### 7. Capacitación
- Fondo: `#f0f2f7`
- Lista vertical de cursos (no grid)
- Cada curso: layout flex con ícono, título, fecha, modalidad badge, vacantes, botón
- Badge modalidad: Verde claro para Virtual, Azul claro para Presencial
- Vacantes < 10: color naranja-ocre; ≥ 10: verde

### 8. Institucional
- Fondo: blanco
- Grid 2 columnas: texto/links izquierda, cards de sedes derecha
- 3 cards de sede: Principal (fondo `#0d2d5e` oscuro), Olivos y Haedo (fondo blanco con borde)
- Sede principal incluye: dirección, teléfono, email, horario

### 9. Contacto
- Fondo: `#f0f2f7`
- Grid 2 columnas: info de contacto | formulario
- Info: cards blancas con datos por área (Administrativa, Técnica)
- Botón WhatsApp: fondo `#25d366`, hover `#1da851`
- Formulario: campos con border `#e0e6f0`, focus `#2563b0`, error `#c0392b`
- Estado enviado: icono check verde + mensaje confirmación

### 10. Footer
- Fondo: `#060f1e`
- Grid 4 columnas: brand | Trámites | Institucional | Servicios
- Logo: mismo PNG con `filter: brightness(0) invert(1)`, height 52px, opacity 0.9
- Links hover: color `#2a9e2a`
- Copyright bar con borde top `rgba(255,255,255,0.1)`

---

## Interacciones y comportamiento

| Elemento | Comportamiento |
|---|---|
| Navbar | Sticky. Al scroll > 40px: oscurece fondo + sombra |
| Hero slider | Auto-rotación cada 6s, indicadores clicables |
| Cards (trámites, noticias, cursos) | `translateY(-4px)` + sombra en hover |
| Botones primarios | Oscurecimiento de color + `translateY(-2px)` en hover |
| Dropdowns navbar | Aparecen en `onMouseEnter`, desaparecen en `onMouseLeave` |
| Formulario | Validación inline (nombre, email requeridos), estado "enviado" con animación |
| WhatsApp | Link a `https://wa.me/541138293041` en nueva pestaña |

---

## Responsividad
- Breakpoint principal: **768px** (mobile) — navbar colapsa a hamburger
- Breakpoint secundario: **900px** — grilla institucional y contacto pasan a 1 columna
- `clamp()` en todos los títulos principales para fluido entre 320px y 1440px

---

## Assets

| Archivo | Uso | Notas |
|---|---|---|
| `assets/logo-cipba-vii.png` | Navbar + Footer | PNG con transparencia. En fondos oscuros: `filter: brightness(0) invert(1)` para versión blanca. En fondos claros: usar tal cual. |

### Íconos
El prototipo usa **íconos SVG inline dibujados a mano** (estilo Feather Icons). En WordPress se puede usar el set **Feather Icons** o **Heroicons** disponibles en Elementor. Los íconos usados son:

`phone`, `mail`, `location`, `clock`, `chevron-right`, `chevron-down`, `external-link`, `award`, `file-text`, `users`, `dollar-sign`, `shield`, `book`, `calendar`, `whatsapp` (custom SVG)

---

## Archivos incluidos

```
design_handoff_cipba/
├── README.md          ← este documento
├── index.html         ← prototipo completo de alta fidelidad
└── assets/
    └── logo-cipba-vii.png
```

---

## Notas para el desarrollador WordPress

1. **Astra Pro**: activar "Sticky Header", configurar Top Bar nativa con teléfono + email. Usar Header Builder para la navbar con megamenú.
2. **Elementor Pro**: construir cada sección como un "Elementor Section" dentro de una Template de página completa (`canvas` page template para evitar márgenes del theme).
3. **El hero slider** puede implementarse con el widget **Slides** de Elementor Pro o con **Smart Slider 3** (plugin gratuito recomendado para más control).
4. **Formulario de contacto**: usar **WPForms Lite** o el widget Form de Elementor. El destino del email debe ser `info@cipba.org`.
5. **Fuentes**: agregar en Astra → Apariencia → Tipografía: **Lato** (cuerpo) y **Roboto Condensed** (títulos).
6. **Colores globales**: cargar el token `--blue-deep: #0d2d5e` y `--green: #2a9e2a` como colores globales en Elementor → Site Settings → Global Colors.
