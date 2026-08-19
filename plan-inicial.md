# Plan: Arranque de la Home en WordPress (setup inicial)

## Contexto
Instalación de WordPress completamente nueva para el sitio de CIPBA Distrito VII. Ya están instalados todos los plugins del stack definido en `README.md` (Astra, Elementor, Max Mega Menu, Smart Slider 3, Fluent/Contact Form 7, CPT UI, ACF, Code Snippets, etc.) y ya existen los archivos del child theme (`astra-cipba-child/`), pero el sitio está vacío: no hay header, menú, hero ni ninguna sección construida todavía. El objetivo es dejar la base técnica lista (theme, tipografías, colores, página Home) para poder empezar a construir las secciones del prototipo `index.html` en orden, siguiendo la metodología ya validada en secciones previas (`plan-seccion-footer.md`, `plan-seccion-contacto.md`, `plan-seccion-quienes-somos.md`, `plan-seccion-resoluciones.md`): widgets **HTML** con `<style>` embebido para estilos locales/hover, y **Apariencia → Personalizar → CSS Adicional** para estilos compartidos y responsive — todo compatible con Elementor Free + Astra Free (sin Custom CSS por widget, que es Pro).

Este plan no modifica nada en el código del sitio; es una guía operativa para el panel de WordPress.

---

## Paso 1 — Verificar el Child Theme y activarlo

1. Confirmar que `astra-cipba-child/style.css` tiene el header obligatorio de child theme:
   ```css
   /*
    Theme Name:   Astra CIPBA Child
    Template:     astra
    Version:      1.0.0
   */
   ```
   El campo `Template: astra` es el que vincula el child theme al theme padre — sin él WordPress no lo reconoce como child theme válido.
2. Confirmar que `functions.php` encola el CSS del padre antes que el del hijo:
   ```php
   add_action('wp_enqueue_scripts', function () {
       wp_enqueue_style('astra-parent-style', get_template_directory_uri() . '/style.css');
       wp_enqueue_style('astra-child-style', get_stylesheet_uri(), ['astra-parent-style']);
   });
   ```
3. **Apariencia → Temas** → activar **Astra CIPBA Child**. Verificar que el sitio carga sin fatal errors (si `functions.php` tiene un error de sintaxis, WordPress puede mostrar pantalla blanca — revisar `debug.log` si pasa).

---

## Paso 2 — Configurar Astra (Personalizar)

En **Apariencia → Personalizar**:

1. **Tipografía → Fuentes de Google**: cargar `Lato` (cuerpo, pesos 300/400/700) y `Roboto Condensed` (títulos, pesos 400/700/900) — Astra Free incluye la librería de Google Fonts nativa.
2. **Global → Contenedor**: ancho de contenedor `1200px` (coincide con `--max-width` del README), tipo Boxed.
3. **Global → Colores**: cargar como colores del tema los tokens base del README (`--blue-deep #0d2d5e`, `--green #2a9e2a`, `--text #1a2540`, etc.) para que estén disponibles como preset también en los color pickers de Astra.
4. **Diseño del sitio → Header**: como el header se va a construir 100% custom con el plugin builder (ver Paso 4), no hace falta tocar el header nativo de Astra — cuando se le asigne el template "Entire Site" al header custom, reemplaza al de Astra automáticamente.

---

## Paso 3 — Colores y tipografía globales en Elementor

En **Elementor → Configuración del sitio** (Site Settings):
- **Global Colors**: reemplazar los 4 colores por defecto por los tokens principales: `#0d2d5e` (Primary/blue-deep), `#2a9e2a` (Secondary/green), `#1a2540` (Text), `#f8f9fc` (blanco/fondo). Esto evita tener que tipear el hex a mano en cada widget.
- **Global Fonts**: definir Primary = Lato (cuerpo) y Secondary = Roboto Condensed (títulos), para reutilizarlas como preset en los widgets Heading.

---

## Paso 4 — Crear la página Home con template Elementor Canvas

1. **Páginas → Añadir nueva** → título `Inicio`.
2. Editar con Elementor. En **Configuración de página** (ícono engranaje abajo a la izquierda) → **Plantilla de página**: **Elementor Canvas** — esto elimina el header/footer nativo de Astra y los márgenes del theme, dejando la página en blanco para que el header/footer custom (Paso 5) sean los únicos visibles.
3. **Ajustes → Lectura** → Tu página de inicio muestra: **Una página estática** → Página de inicio: `Inicio`.

---

## Paso 5 — Preparar Header y Footer globales (antes de las secciones de contenido)

El README marca el header (Top Bar + Navbar sticky) y el footer como **compartidos entre todas las páginas**, así que conviene resolverlos antes de avanzar con el contenido de la Home:

- **Plugin**: mismo que usa `plan-seccion-footer.md` — *"Ultimate Addons for Elementor (UAE)"* (Brainstorm Force, gratuito; slug `header-footer-elementor`). Es el sucesor de "Elementor Header & Footer Builder" / "Header Footer & Blocks for Elementor" — mismas funciones, plugin renombrado. Habilita plantillas globales de Header y Footer en Elementor Free (sin esto, Theme Builder es función Pro).
- **Footer**: ya está completamente especificado en `plan-seccion-footer.md` — seguirlo tal cual (**UAE → Header & Footer Builder → Add New**, Display Location: Entire Site).
- **Header**: no hay un `plan-seccion-*.md` dedicado todavía (se construyó de forma ad-hoc en una sesión anterior, registrada en `wpplan-chat.md`). Para esta primera pasada, armar el Header como plantilla nueva (**UAE → Header & Footer Builder → Add New**, tipo Header, Display Location: Entire Site) cubriendo:
  - **Top Bar** (README sección 1): fondo `#0d2d5e`, teléfono/email/horario a la izquierda, WhatsApp + "Consejo Superior" a la derecha.
  - **Navbar sticky** (README sección 2): logo, links + dropdowns (usar **Max Mega Menu** para el ítem "Institucional"), botón CTA "Visado Online". El comportamiento sticky con cambio de fondo al hacer scroll requiere **myStickymenu** + CSS con la clase `.is-sticky` (ver tabla de workarounds del README).

Si más adelante se quiere, se puede formalizar esto en un `plan-seccion-header-navbar.md` con el mismo nivel de detalle que el resto — queda pendiente, fuera del alcance de este arranque.

---

## Paso 6 — Orden recomendado para las secciones de la Home

Con el Header, Footer y la página base ya andando, construir el resto de `index.html` en este orden (según numeración del README):

| # | Sección | Estado |
|---|---|---|
| 3 | Hero (slider 3 slides) | A construir — Smart Slider 3, ver README sección 3 |
| — | Stats strip | A construir — ver `wpplan-chat.md` (ya resuelto en sesión anterior, Elementor Free puro) |
| 4 | Acceso Rápido / Trámites | A construir — ver `wpplan-chat.md` |
| 5 | Noticias | A construir — ver `wpplan-chat.md` (CPT Posts + Essential Addons Post Grid) |
| 6 | Banner Visado Online | A construir — ver `wpplan-chat.md` (estático, Elementor Free puro) |
| 7 | Capacitación / Próximos cursos | A construir — ver `wpplan-chat.md` (CPT `curso` + ACF + shortcode) |
| 8 | Normativa / Resoluciones | Ya especificado en `plan-seccion-resoluciones.md` |
| 9 | Institucional (resumen en Home) | Ya especificado en `plan-seccion-quienes-somos.md` |
| 10 | Contacto | Ya especificado en `plan-seccion-contacto.md` |
| 11 | Footer | Ya especificado en `plan-seccion-footer.md` (global, Paso 5) |

Cada sección se agrega como una nueva **Section** de Elementor dentro de la página `Inicio`, en el mismo orden del prototipo.

---

## Verificación del setup inicial

1. El sitio carga con el child theme activo, sin errores PHP.
2. La página `Inicio` abre con plantilla Elementor Canvas: no debe verse header/footer de Astra, solo lo que se agregue en el editor.
3. Los Global Colors y Global Fonts configurados en Elementor aparecen como preset al crear un widget Heading nuevo.
4. Las fuentes Lato y Roboto Condensed se ven aplicadas (inspeccionar con DevTools → Computed → font-family).
5. Una vez armado el Header y Footer como plantillas "Entire Site", verificar que aparecen en cualquier página nueva sin tener que agregarlos manualmente.
