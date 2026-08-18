# Handoff: CIPBA Distrito VII

## Overview
Rediseño del sitio institucional del **Colegio de Ingenieros de la Provincia de Buenos Aires – Distrito VII** (cipba.org).

Este handoff incluye dos páginas completas de alta fidelidad:

| Página | Archivo | Contenido |
|---|---|---|
| **Home** | `index.html` | Hero con slider, accesos rápidos, noticias, banner Visado, capacitación, reglamentaciones, institucional resumido, contacto |
| **Institucional** | `institucional.html` | Autoridades del Consejo Directivo 2024-2027, 23 partidos del distrito (con mapa visual) y 4 sedes con contactos por área |

Ambas páginas comparten navbar, footer, design tokens y comportamiento responsive.

## Sobre los archivos de diseño
Los archivos `index.html` e `institucional.html` son **prototipos de alta fidelidad creados en HTML/React**. Son referencias visuales y de comportamiento — **no son código de producción para copiar directamente**. La tarea del desarrollador es recrear estos diseños en WordPress usando el theme y page builder elegidos (recomendado: **Astra Pro + Elementor Pro**), respetando los tokens de diseño, layouts y comportamientos documentados aquí.

## Fidelidad
**Alta fidelidad (hifi)**: colores, tipografías, espaciados e interacciones son finales. El desarrollador debe recrear la UI pixel a pixel usando las herramientas de WordPress.

---

## Stack WordPress recomendado
| Componente | Recomendación |
|---|---|
| Theme base | **Astra Pro** |
| Page builder | **Elementor Pro** |
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

## Secciones de la Home (`index.html`)

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
- Normativa
- Institucional (dropdown: Autoridades, Historia, Delegaciones)
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

### 8. Reglamentaciones y Resoluciones (Normativa)
- Sección `id="normativa"`, fondo blanco, padding `60px 24px`
- Header con eyebrow verde "Marco normativo", título principal y descripción
- **Toolbar superior** con:
  - Campo de búsqueda con icono lupa (busca por título o número de documento)
  - Chips de filtro por categoría (Todas + categorías dinámicas)
  - Chip activo: fondo `#0d2d5e` blanco; inactivo: fondo blanco texto gris con borde `#e0e6f0`
- **Contador de resultados** debajo de la toolbar (12.5px gris)
- **Lista de documentos** dentro de un contenedor con borde redondeado `#e8f1fc`:
  - Cada fila: grid `52px 1fr auto auto auto` con gap 16px y padding `16px 20px`
  - Separador entre filas: borde inferior `1px solid #e8f1fc`
  - **Ícono PDF**: tarjeta 44×52px con fondo tintado en color de categoría (12% opacity), icono file-text + label "PDF" en color de categoría
  - **Título y meta**: badge de categoría coloreado, número ("Resolución CS 187/2026") en Roboto Condensed, título 14.5px weight 700
  - **Fecha**: icono calendar + fecha, 13px gris (oculto en mobile)
  - **Tamaño**: "12 pág · 342 KB" en Roboto Condensed 12px (oculto en mobile)
  - **Acciones**: botón "Ver" (outline, color de categoría) + botón "PDF" (fondo `#0d2d5e`, descarga)
- **Categorías y colores**:
  - Honorarios: `#8a1a1a`
  - Visado: `#2563b0`
  - Institucional: `#0d2d5e`
  - Matrícula: `#1a8a4a`
  - Capacitación: `#7a1a8a`
- **Tipos de documento**: Resolución, Reglamento, Disposición
- **Vista previa expandible** al hacer click en "Ver":
  - Grid 2 columnas: `1fr 280px` (en mobile pasa a 1 columna)
  - Izquierda: PDF simulado (fondo blanco, borde `#d0d8e8`, font Georgia serif, encabezado con border bottom color categoría, contenido tipo "VISTO / CONSIDERANDO")
  - Derecha: panel de metadatos con Tipo, Número, Categoría, Fecha, Páginas, Tamaño, Estado, botón "Descargar PDF completo"
- **Estado vacío**: si no hay resultados, mensaje centrado "No se encontraron documentos con esos criterios"

**Implementación WordPress sugerida**:
- **Custom Post Type** "Resoluciones" con campos ACF: número, tipo, fecha, categoría (taxonomy), archivo PDF, páginas, tamaño, estado
- **Plugin recomendado**: **WP Document Revisions** o **PublishPress Capabilities** para gestionar versiones y permisos
- **Filtros/búsqueda**: **FacetWP** o **Search & Filter Pro** para buscar y filtrar sin recargar página
- **Vista previa PDF**: **PDF Embedder** (free) o **PDF.js Viewer** para mostrar el PDF embebido. Para una vista previa rápida (sin cargar el PDF completo) se puede generar una imagen de la primera página con **ImageMagick** + Ghostscript al subir el archivo, y mostrarla en lugar del HTML decorativo del prototipo
- **Categorías**: usar `register_taxonomy()` con colores asignados vía ACF al término

### 9. Institucional
- Fondo: blanco
- Grid 2 columnas: texto/links izquierda, cards de sedes derecha
- 3 cards de sede: Principal (fondo `#0d2d5e` oscuro), Olivos y Haedo (fondo blanco con borde)
- Sede principal incluye: dirección, teléfono, email, horario

### 10. Contacto
- Fondo: `#f0f2f7`
- Grid 2 columnas: info de contacto | formulario
- Info: cards blancas con datos por área (Administrativa, Técnica)
- Botón WhatsApp: fondo `#25d366`, hover `#1da851`
- Formulario: campos con border `#e0e6f0`, focus `#2563b0`, error `#c0392b`
- Estado enviado: icono check verde + mensaje confirmación

### 11. Footer (compartido entre páginas)
- Fondo: `#060f1e`
- Grid 4 columnas: brand | Trámites | Institucional | Servicios
- Logo: PNG invertido a blanco (`filter: brightness(0) invert(1)`), height 52px, opacity 0.9
- Links hover: color `#2a9e2a`
- Copyright bar con borde top `rgba(255,255,255,0.1)`

---

## Página Institucional (`institucional.html`)

Página interna accesible desde el navbar (link "Institucional"). Comparte TopBar, Navbar y Footer con la home. El item "Institucional" del navbar aparece marcado como activo con fondo verde tintado `rgba(42,158,42,0.25)` y border bottom `2px solid #2a9e2a`.

### I.1. Page Hero (cabecera de página interna)
- Fondo: gradiente `linear-gradient(135deg, #0d2d5e 0%, #1a4a8a 60%, #2563b0 100%)` con patrón SVG decorativo opacity 0.06
- Padding: `48px 24px 56px`
- **Breadcrumb** arriba (13px, `rgba(255,255,255,0.65)`):
  - Ícono home + "Inicio" (link) › "Institucional" (activo, blanco bold)
- Badge eyebrow: "Quiénes somos" con punto verde, fondo `rgba(42,158,42,0.22)`
- H1: "Distrito VII" en Roboto Condensed, clamp 28–48px, weight 900, blanco, letter-spacing -0.5
- Párrafo descriptivo (17px, `rgba(255,255,255,0.82)`, max-width 720px)
- **Quick nav chips** (anclas internas): Autoridades, Partidos comprendidos, Sedes y delegaciones
  - Fondo: `rgba(255,255,255,0.1)`, border `rgba(255,255,255,0.25)`
  - Hover: fondo verde `rgba(42,158,42,0.4)`, border `#2a9e2a`

### I.2. Autoridades (Consejo Directivo)
- Sección `id="autoridades"`, fondo blanco, padding `64px 24px`
- Header centrado: eyebrow verde con icono users + título "Autoridades" + pill azul "Período 2024 – 2027"
- **Grid**: `repeat(auto-fill, minmax(280px, 1fr))`, gap 18px
- **Card del Presidente** (destacada):
  - Ocupa `grid-column: span 2`
  - Fondo gradiente azul `linear-gradient(135deg, #0d2d5e 0%, #1a4a8a 100%)`, texto blanco
  - Badge "Presidencia" en esquina superior derecha con icono star y fondo verde `#2a9e2a`
  - Avatar circular grande 72×72px con gradiente verde y borde blanco semitransparente, conteniendo iniciales en Roboto Condensed 22px weight 900
  - Cargo (label verde claro), nombre (19px weight 800 blanco), título profesional (itálica)
- **Cards de Secretario, Tesorero, Vocales** (8 cards):
  - Fondo blanco, border `#e8f1fc`, border-radius 12px
  - Avatar circular 56×56px con gradiente azul claro `linear-gradient(135deg, #e8f1fc, #c8d8f0)` y iniciales azules en Roboto Condensed 18px
  - Hover: `translateY(-3px)`, sombra suave, border `#2a9e2a`
  - Layout: avatar a la izquierda + bloque de texto a la derecha (cargo, nombre, título profesional)

**Datos a cargar (Consejo Directivo 2024 – 2027):**
| Cargo | Nombre | Título profesional |
|---|---|---|
| Presidente | Daniel Héctor PALACIOS | Ing. Electricista y Laboral |
| Secretario | Fabián José Miguel PORCILE | Ing. Civil |
| Tesorero | Marina Helena VACA | Inga. Civil |
| Vocal Titular 1° | Gabriel Esteban BUSNARDO | Ing. en Alimentos |
| Vocal Titular 2° | Mariano Alejandro PRALONG | Ing. Civil |
| Vocal Titular 3° | Fabián Roberto MONTERO | Ing. Civil |
| Vocal Suplente 1° | Juan José URANGA | Ing. Mecánico |
| Vocal Suplente 2° | Perla Beatriz ARMAGNAC | Inga. Civil |
| Vocal Suplente 3° | María Claudia FILIPUZZI | Inga. en Ecología |

**Implementación WordPress sugerida:**
- **Custom Post Type** "Autoridades" con ACF: cargo (select), nombre, título profesional, orden, destacado (boolean), foto (opcional)
- Loop ordenado por campo `orden` con primer item destacado renderizando el layout grande
- Si en el futuro se quieren cargar fotos reales, sustituir el avatar de iniciales por la imagen

### I.3. Partidos comprendidos
- Sección `id="partidos"`, fondo `#f0f2f7`, padding `64px 24px`
- Header centrado: eyebrow verde con icono location + "Jurisdicción" + título "Partidos comprendidos" + descripción con counts destacados
- **Layout grid**: `1fr 1.4fr` (mapa | listado). En mobile (≤ 900px) pasa a 1 columna
- **Mapa visual** (panel izquierdo):
  - Card blanca sticky (`top: 88px`), border-radius 12px, sombra suave
  - SVG `viewBox="0 0 320 340"` con:
    - Polígono outline del distrito en gradiente azul claro `#e8f1fc → #d4e6f7`, stroke verde `#2a9e2a` 2.5px
    - Pinpoints (círculos azules `#0d2d5e` radio 3.5px) en posiciones aproximadas de los partidos
    - San Justo destacado: círculo verde grande `#2a9e2a` radio 6px con halo, callout-line + rectángulo verde con texto "★ SAN JUSTO" en Roboto Condensed
    - Texto inferior gris itálica: "Distribución aproximada · No a escala"
  - Card inferior con badge "Sede principal: San Justo · La Matanza"
- **Listado de partidos** (panel derecho):
  - Card blanca con campo de búsqueda en vivo (filtra por nombre)
  - Grid: `repeat(auto-fill, minmax(160px, 1fr))`, gap 8px
  - Cada chip: fondo `#f8f9fc`, punto verde `#2a9e2a`, nombre del partido 13.5px
  - Hover: fondo `#e8f5ee`, border `#2a9e2a`, texto `#0d2d5e`
  - Contador dinámico de resultados

**Lista de 23 partidos:**
Escobar, Exaltación de la Cruz, General Las Heras, General Rodríguez, General San Martín, Hurlingham, Ituzaingó, José C. Paz, La Matanza, Luján, Malvinas Argentinas, Marcos Paz, Mercedes, Merlo, Moreno, Morón, Pilar, San Isidro, San Fernando, San Miguel, Tigre, Tres de Febrero, Vicente López.

**Implementación WordPress sugerida:**
- **CPT** "Partidos" o simplemente array estático (los datos rara vez cambian)
- El mapa SVG es decorativo — se puede recrear pixel a pixel en Elementor con widget HTML, o reemplazar por un mapa real con **WP Google Maps Pro** con marcadores en cada partido
- Búsqueda en vivo: JavaScript inline simple con `addEventListener('input')` sobre los chips

### I.4. Sedes y delegaciones
- Sección `id="sedes"`, fondo blanco, padding `64px 24px`
- Header centrado: eyebrow + título "Sedes y delegaciones" + descripción
- **Grid**: `repeat(auto-fill, minmax(280px, 1fr))`, gap 18px
- **Card de Sede Central San Justo** (destacada):
  - Ocupa `grid-column: 1 / -1` (todo el ancho)
  - Fondo gradiente azul `linear-gradient(135deg, #0d2d5e 0%, #1a4a8a 100%)`, padding 32px
  - Sombra: `0 12px 40px rgba(13,45,94,0.18)`
  - Halo decorativo verde en esquina superior derecha (`radial-gradient` con `rgba(42,158,42,0.25)`)
  - Header: tag eyebrow + h3 "Sede San Justo" (Roboto Condensed 28px weight 900) + badge verde "★ Casa Central"
  - **Layout 2 columnas**: info izquierda | contactos por área derecha
  - Info: filas con icono cuadrado 28×28px fondo `rgba(255,255,255,0.1)`, label uppercase pequeño, valor 14px blanco. Separadores `1px solid rgba(255,255,255,0.1)`
  - Contactos: lista con scroll (max-height 420px), cada item card `rgba(255,255,255,0.06)` con nombre + badge verde de rol + tel + email
- **Cards de delegaciones** (3, no destacadas):
  - Fondo blanco, border `#e8f1fc`, padding `24px 26px`
  - Tag eyebrow verde, h3 19px weight 900
  - Filas info con icono azul `#2563b0` y separador dashed

**Datos de las sedes:**

**Sede San Justo (Central)**
- Dirección: Almafuerte N° 2868, San Justo (1754) – La Matanza – Bs As
- Teléfono: (011) 3535-0751
- Email: info@cipba.org
- Horario: Lunes a viernes de 9:00 a 16:00 hs
- Contactos directos por área (Administración, Secretaría, Tesorería, Técnica, Gerencia Técnica) — 7 referentes con teléfono celular y email

**Parque Industrial DECA (Haedo)**
- Dirección: Valentín Gómez N° 577 1° of. 1, Haedo
- Teléfono: (011) 5433-5344
- Horario: Lunes a viernes de 9:00 a 15:00 hs

**Vicente López (Olivos)**
- Dirección: Ricardo Gutiérrez N° 1834 (CP 1636), Olivos
- Teléfono: (011) 7398-2119
- Horario: Sólo correspondencia

**General Rodríguez**
- Dirección: Av. España 493 – Gral. Rodríguez
- Teléfono: (011) 2563-1616
- Visador: Ing. Civil Darío Kubar (Mat. 51785)
- Email: cipba7gr@gmail.com
- Horario: Lunes a viernes de 9:00 a 13:00 hs. Visador en el mismo horario.

**Implementación WordPress sugerida:**
- **CPT** "Sedes" con ACF: nombre, tag, destacada (boolean), dirección, teléfono, email, visador, horario, repeater de contactos (rol, nombre, tel, email)
- Plantilla única para sede destacada y secundarias — condicional `if (destacada)` cambia layout y colores

### I.5. CTA Final (banner verde)
- Fondo: gradiente verde `linear-gradient(135deg, #2a9e2a 0%, #1f7a1f 100%)`
- Padding: `48px 24px`, contenido centrado max-width 900px
- Título blanco Roboto Condensed clamp 20–28px + párrafo gris claro
- Dos botones:
  - Primario: fondo blanco, texto `#1f7a1f`, "Formulario de contacto" → ancla a home `index.html#contacto`
  - Secundario outline: fondo `rgba(255,255,255,0.15)`, icono WhatsApp + texto, link a `wa.me/541138293041`

---

## Notas de navegación entre páginas

- El `index.html` enlaza a `institucional.html` desde el item "Institucional" del navbar (con su dropdown apuntando a las anclas internas)
- El `institucional.html` enlaza de vuelta a `index.html` desde:
  - El logo
  - Todos los items del navbar excepto "Institucional"
  - El breadcrumb ("Inicio")
  - El CTA final ("Formulario de contacto")
  - Los links del footer
- En el navbar de `institucional.html` el item "Institucional" está marcado como activo (estilo distinto: fondo verde tintado, weight 800, border bottom verde)

### 11. Footer
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

`phone`, `mail`, `location`, `clock`, `chevron-right`, `chevron-down`, `external-link`, `award`, `file-text`, `users`, `dollar-sign`, `shield`, `book`, `calendar`, `search`, `eye`, `download`, `whatsapp` (custom SVG)

---

## Archivos incluidos

```
design_handoff_cipba/
├── README.md           ← este documento
├── index.html          ← prototipo Home (alta fidelidad)
├── institucional.html  ← prototipo Institucional (alta fidelidad)
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
