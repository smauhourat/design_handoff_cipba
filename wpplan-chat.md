╭─── Claude Code v2.1.128 ─────────────────────────────────────────────────────╮
│                                                    │ Tips for getting        │
│                    Welcome back!                   │ started                 │
│                                                    │ Run /init to create a … │
│                       ▐▛███▜▌                      │ ─────────────────────── │
│                      ▝▜█████▛▘                     │ What's new              │
│                        ▘▘ ▝▝                       │ Internal fixes          │
│    Sonnet 4.6 · Claude Pro ·                       │ [VSCode] Fixed extensi… │
│    santiago.mauhourat@gmail.com's Organization     │ Added `CLAUDE_CODE_ENA… │
│ D:\Projects\ColegioIngenierosPBA\web\ColegioIngPb… │ /release-notes for more │
╰──────────────────────────────────────────────────────────────────────────────╯

❯ utiliza el readme para tener contexto, ya tengo montado mi wordpress en un    
  docker y tengo armado header, menu y seccion hero.                            
  Necestito que me indiques como seguir para agregar las secciones siguientes:  
  Stats strip                                                                   
  ⎿  ⧉ Selected 1 lines from index.html in Visual Studio Code

● Voy a leer el README y el index.html para tener contexto completo del
  proyecto.

  Searched for 1 pattern, read 2 files (ctrl+o to expand)

● Perfecto, ya tengo todo el contexto. El Stats Strip está justo debajo del hero
   y es una banda blanca con 4 estadísticas en columnas. Te explico cómo
  implementarlo en Elementor Pro:

  ---
  Stats Strip en Elementor Pro

  Diseño de referencia (del prototipo)

  - Fondo: blanco
  - Sombra inferior: 0 4px 20px rgba(0,0,0,0.06)
  - Border bottom: 1px solid #e8f1fc
  - 4 columnas iguales, separadas por divisores #e8f1fc
  - Número: 26px, peso 900, #0d2d5e, Roboto Condensed
  - Label: 12px, #9aa5b8

  ---
  Paso a paso en Elementor

  1. Agregar nueva sección debajo del hero
  - En Elementor, hacé clic en el + debajo de la sección del hero
  - Elegí estructura de 4 columnas iguales

  2. Configurar la sección (Section Settings)
  - Layout → Content Width: Boxed, 1200px
  - Style → Background: Color sólido #ffffff
  - Style → Border → Bottom: 1px, color #e8f1fc
  - Style → Box Shadow: 0 4px 20px rgba(0,0,0,0.06) (Horizontal 0, Vertical 4,
  Blur 20, Spread 0, Color rgba(0,0,0,0.06))
  - Layout → Padding: Top 0, Bottom 0 (el padding va en las columnas)

  3. Configurar cada columna
  - Advanced → Padding: 20px top/bottom, 16px left/right
  - Style → Border → Right: 1px, color #e8f1fc (en las primeras 3 columnas; la
  4ta sin borde)

  4. Dentro de cada columna: widget Heading para el número
  - Texto: +8.500 / 24 / 3 / +30
  - Style → Typography: Roboto Condensed, 26px, peso 900
  - Style → Text Color: #0d2d5e
  - Advanced → Margin: 0
  - Alignment: Center

  5. Debajo del número: widget Text Editor para el label
  - Texto: Matriculados activos / Partidos del Distrito VII / Sedes de atención
  / Años de trayectoria
  - Style → Typography: Lato, 12px, peso 400, letter-spacing 0.3px
  - Style → Text Color: #9aa5b8
  - Advanced → Margin: Top 3px
  - Alignment: Center

  ---
  Contenido de los 4 stats

  ┌─────┬────────┬───────────────────────────┐
  │  #  │ Número │           Label           │
  ├─────┼────────┼───────────────────────────┤
  │ 1   │ +8.500 │ Matriculados activos      │
  ├─────┼────────┼───────────────────────────┤
  │ 2   │ 24     │ Partidos del Distrito VII │
  ├─────┼────────┼───────────────────────────┤
  │ 3   │ 3      │ Sedes de atención         │
  ├─────┼────────┼───────────────────────────┤
  │ 4   │ +30    │ Años de trayectoria       │
  └─────┴────────┴───────────────────────────┘

  ---
  Tip para el separador de columnas

  Elementor no tiene un divisor vertical nativo entre columnas. La forma más
  limpia es usar el border right en las primeras 3 columnas. Si el borde no se
  ve bien, como alternativa podés agregar un widget Divider rotado 90°, pero el
  border de columna es más limpio.

  Una vez que tengas el Stats Strip listo, la siguiente sección es el Acceso 
  Rápido / Trámites (sección 4 del README) — grid de 6 cards con íconos sobre
  fondo #f0f2f7.

✻ Cooked for 33s

❯ modifique el readme,  pore es Elemento Free y Astra Free                      

● Déjame leer el README actualizado.

  Read 1 file (ctrl+o to expand)

● Confirmado. Con Elementor Free + Astra Free hay algunas limitaciones clave
  para el Stats Strip. Te actualizo las instrucciones:

  ---
  Stats Strip — Elementor Free + Astra Free

  Limitaciones relevantes

  - Box Shadow en secciones no está disponible en Elementor Free (es feature
  Pro)
  - Padding por columna individual está disponible en Free
  - No hay widget de contador animado en Free (se pone el número como texto
  estático)

  ---
  Paso a paso adaptado

  1. Nueva sección con 4 columnas
  - Clic en + debajo del hero → estructura 4 columnas iguales

  2. Configurar la sección
  - Layout → Content Width: Boxed, 1200px
  - Style → Background Color: #ffffff
  - Layout → Padding: 0 en todos los lados

  ▎ La sombra (box-shadow) y el border-bottom no se pueden hacer desde el panel 
  ▎ de Elementor Free. Se resuelven con CSS personalizado (ver abajo).

  3. CSS personalizado para la sección
  - En la sección: Advanced → Custom CSS
  selector {
    box-shadow: 0 4px 20px rgba(0,0,0,0.06);
    border-bottom: 1px solid #e8f1fc;
  }

  4. Cada columna: padding y separador
  - Advanced → Padding: 20px top/bottom, 16px left/right
  - Para el divisor entre columnas, en las primeras 3: Advanced → Custom CSS
  selector {
    border-right: 1px solid #e8f1fc;
  }

  5. Widget Heading para el número
  - Tipo: H3 (semántica apropiada)
  - Texto: +8.500, 24, 3, +30
  - Style → Typography: Roboto Condensed, 26px, 900
  - Style → Text Color: #0d2d5e
  - Alignment: Center

  6. Widget Text Editor para el label
  - Texto: el label correspondiente
  - Style → Typography: Lato, 12px, Normal, letter-spacing 0.3
  - Style → Text Color: #9aa5b8
  - Advanced → Margin: Top 3px
  - Alignment: Center

  ---
  Alternativa sin CSS custom para la sombra

  Si preferís evitar el CSS custom por ahora, podés dejarlo sin sombra — el
  border-bottom: 1px solid #e8f1fc sí se puede hacer agregando un widget Divider
   al final de la sección como separador visual.

  ---
  Guardá la memoria de que usan Elementor Free y Astra Free.

  Searched memories, wrote 2 memories (ctrl+o to expand)

● Memoria guardada. De ahora en más todas las instrucciones van ajustadas a
  Free. El Advanced → Custom CSS es tu mejor aliado para los efectos que no
  expone el panel visual.

✻ Sautéed for 54s

※ recap: Estás construyendo la home de CIPBA en WordPress con Elementor Free y Astra Free siguiendo el prototipo HTML del handoff. Terminaste el Stats Strip; el próximo paso es agregar la sección Acceso Rápido con grid de 6 cards sobre fondo #f0f2f7. (disable recaps in /config)

❯ Como armo la seccionde noticias en wordpress                                  
  ⎿  ⧉ Selected 1 lines from index.html in Visual Studio Code

● Déjame leer el código de la sección Noticias del prototipo.

  Searched for 1 pattern, read 1 file (ctrl+o to expand)

● Tengo todo el detalle. Para la sección de Noticias hay una decisión clave
  antes de empezar:

  ---
  Sección Noticias — Decisión previa

  Las noticias deberían ser WordPress Posts reales (dinámicos) para que el
  cliente pueda cargarlas desde el panel sin tocar Elementor. Elementor Free
  tiene un widget Posts pero es muy limitado en estilos.

  Recomendación: instalar Essential Addons for Elementor (gratis) — incluye el
  widget Post Grid con mucho más control de diseño.

  ---
  Parte 1: Preparar WordPress Posts

  1. Categorías de noticias (Entradas → Categorías):
  - Institucional
  - Capacitación
  - Normativa
  - Visado

  2. Cargar las 4 noticias del prototipo como Entradas normales, asignando
  categoría a cada una. La "destacada" se puede marcar con una entrada fijada
  (sticky post).

  ---
  Parte 2: Construir la sección en Elementor

  Estructura de la sección

  Sección (fondo blanco, padding 60px top/bottom)
    └── Columna única 1200px
          ├── Fila header: subtítulo + H2 + link "Archivo completo"
          └── Post Grid (Essential Addons)

  ---
  Header de la sección

  Columna 1 (ancho 1200px)

  Widget Heading para el supertítulo:
  - Texto: NOVEDADES
  - Tag: p
  - Typography: Lato, 12px, 700, letter-spacing 2px, uppercase
  - Color: #2a9e2a
  - Margin bottom: 8px

  Widget Heading para el título principal:
  - Texto: Noticias del Distrito
  - Tag: H2
  - Typography: Roboto Condensed, clamp(22px, 3vw, 30px), 900
  - Color: #0d2d5e

  Para el link "Archivo completo →" a la derecha, lo más simple en Free es un
  widget Button o Text Editor alineado a la derecha, con color #2563b0.

  ▎ En Elementor Free no podés hacer fácilmente flex space-between en el header 
  ▎ row. Alternativa: dos columnas dentro de una inner section — izquierda con 
  ▎ los textos, derecha con el link alineado al centro/bottom.

  ---
  Post Grid con Essential Addons

  Una vez instalado el plugin:

  1. Agregar widget EA Post Grid
  2. Content → Query:
    - Post Type: Posts
    - Posts per page: 4
    - Order by: Date DESC
  3. Content → Layout: Grid, 4 columnas (desktop), 2 (tablet), 1 (mobile)
  4. Style → Card:
    - Border radius: 10px
    - Border: 1px solid #e8f1fc
    - Box shadow: 0 2px 8px rgba(0,0,0,0.04)
  5. Style → Category Badge: pill, tamaño 11px, peso 700
  6. Style → Title: 15.5px, peso 800, color #1a2540
  7. Style → Excerpt: 13.5px, color #6b7a99, line-height 1.6
  8. Style → Read More: color #2563b0, 13px, 700

  El border-top de color por categoría no se puede hacer nativamente con el Post
   Grid. Se hace con CSS custom:

  /* Border top por categoría */
  .eael-post-grid .eael-grid-post[class*="category-institucional"]
  .eael-grid-post-holder {
    border-top: 3px solid #0d2d5e;
  }
  .eael-post-grid .eael-grid-post[class*="category-capacitacion"]
  .eael-grid-post-holder {
    border-top: 3px solid #1a8a4a;
  }
  .eael-post-grid .eael-grid-post[class*="category-normativa"]
  .eael-grid-post-holder {
    border-top: 3px solid #8a1a1a;
  }
  .eael-post-grid .eael-grid-post[class*="category-visado"]
  .eael-grid-post-holder {
    border-top: 3px solid #2563b0;
  }

  Este CSS va en Apariencia → Personalizar → CSS adicional (o en el widget mismo
   si tiene campo CSS).

  ---
  Hover effect

  El translateY(-3px) en hover también va en CSS adicional:

  .eael-post-grid .eael-grid-post-holder {
    transition: all 0.25s;
  }
  .eael-post-grid .eael-grid-post-holder:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 28px rgba(0,0,0,0.10);
  }

  ---
  Card "Destacado"

  La entrada fijada (sticky) aparece primero. Para el banner azul #0d2d5e con
  "📌 Destacado", EA Post Grid Free no lo soporta nativamente. Por ahora podés
  omitirlo o agregarlo como CSS apuntando a .sticky:

  .eael-post-grid .post.sticky .eael-grid-post-holder::before {
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

  ---
  Resumen del flujo: crear categorías → cargar entradas → instalar Essential
  Addons → armar la sección con Post Grid + ajustes de estilo + CSS para bordes
  y hover.

✻ Churned for 56s

※ recap: Building the CIPBA homepage in WordPress with Elementor Free and Astra Free. Currently implementing the Noticias section. Next step: install Essential Addons for Elementor (free) to get the Post Grid widget. (disable recaps in /config)

❯ pero el essentials addons de elementor es free?                               

● Sí, tiene versión gratuita disponible en el repositorio oficial de WordPress
  (wordpress.org/plugins/essential-addons-for-elementor-lite). El plugin se
  llama Essential Addons for Elementor – Best Elementor Addons (el "lite").

  La versión free incluye el widget Post Grid que es el que necesitás. La
  versión Pro agrega widgets extra (timeline, data table, etc.) pero no la
  necesitás para este caso.

  Se instala directo desde WordPress: Plugins → Añadir nuevo → buscar "Essential
   Addons for Elementor".

✻ Churned for 6s

❯ .post.sticky no aparece                                                       

● Es porque Essential Addons Post Grid no aplica la clase .sticky de WordPress
  en su HTML propio. Tenés que inspeccionar el elemento real con DevTools para
  encontrar la clase exacta.

  Cómo hacerlo:

  1. En el navegador, clic derecho sobre la card destacada → Inspeccionar
  2. Buscá en el HTML el elemento <article> o el div contenedor de esa card
  3. Fijate qué clases tiene — probablemente algo como .eael-grid-post con
  alguna clase adicional

  Mandame un screenshot o copiame las clases que aparecen en ese elemento y te
  doy el selector CSS exacto.

  ---
  Alternativa más simple si no aparece ninguna clase útil:

  Dado que la card destacada es siempre la primera, podés apuntarla por
  posición:

  .eael-post-grid .eael-post-grid-wrap .eael-grid-post:first-child
  .eael-grid-post-holder::before {
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

  Esto funciona mientras la entrada fijada siga siendo la más reciente (que con
  Order by: Date DESC siempre va primero).

✻ Worked for 16s

※ recap: Están construyendo la home de CIPBA en WordPress con Elementor Free y Astra Free. La sección de Noticias está casi lista — el próximo paso es que el usuario inspeccione el HTML de la card destacada con DevTools para encontrar el selector CSS correcto del banner "Destacado". (disable recaps in /config)

❯ no me sirve la alternativa, necesito identificar los posts fijados            

● El problema es que EA Post Grid no siempre pasa la clase sticky de WordPress a
   su HTML. La solución más limpia es un snippet de JavaScript que consulta la
  REST API de WordPress.

  Paso 1: Verificar que el post esté fijado

  En Entradas → Todas las entradas, el post destacado debe mostrar la etiqueta
  "Fijado" debajo del título. Si no la tiene, editalo → panel derecho → Opciones
   de entrada → Fijar esta entrada en la parte superior del blog.

  ---
  Paso 2: Probar primero con selector simple

  Antes del JS, probá este CSS — EA sí incluye post_class() de WordPress en el
  <article>, que debería tener sticky:

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

  ---
  Paso 3: Si aún no funciona → JavaScript via REST API

  Instalá el plugin Code Snippets (gratis, wordpress.org) y agregá este snippet
  de tipo JavaScript:

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

  Y en CSS adicional:

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

  ---
  Probá primero el Paso 2 — si el post está correctamente fijado en WP ese
  selector debería ser suficiente.

✻ Worked for 26s
❯ Sigamos con la seccion siguiente, la que tiene como texto principal "Visado   
  de trabajos profesionales 100% online"                                        

● Déjame leer el código completo del VisadoBanner.

  Read 1 file (ctrl+o to expand)

● Tengo todo. Esta sección es puramente estática (no trae datos dinámicos), así
  que se arma 100% con Elementor Free sin plugins extra.

  ---
  Banner Visado — Elementor Free

  Estructura visual

  Dos columnas sobre gradiente azul:
  - Izquierda: supertítulo + H2 + párrafo
  - Derecha: lista de 4 features con checkmark + botón CTA

  ---
  1. Configurar la sección

  - Layout → Content Width: Boxed, 1200px
  - Layout → Padding: 52px top/bottom, 24px left/right
  - Style → Background: Gradiente
    - Tipo: Linear, ángulo 135°
    - Color 1: #0d2d5e posición 0%
    - Color 2: #1a4a8a posición 100%

  ---
  2. Columna izquierda

  Widget Heading — supertítulo:
  - Texto: SISTEMA ONLINE
  - Tag: p
  - Typography: Lato, 12px, 700, letter-spacing 2px, uppercase
  - Color: #d4f0d4
  - Margin bottom: 12px

  Widget Heading — título principal:
  - Texto: Visado de trabajos profesionales 100% online
  - Tag: H2
  - Typography: Roboto Condensed, clamp(22px, 3vw, 34px), 900, line-height 1.2
  - Color: #ffffff
  - Margin bottom: 16px

  Widget Text Editor — párrafo:
  - Texto: Realizá el visado de tus trabajos desde cualquier dispositivo, las 24
   horas. Con 20% de descuento en la tasa de visado respecto al trámite 
  presencial.
  - Typography: Lato, 16px, 400, line-height 1.65
  - Color: rgba(255,255,255,0.75)

  ---
  3. Columna derecha — lista de features

  Cada feature es un widget Icon List. Agregá un solo widget con los 4 ítems:

  ┌───────────────────────────────────┐
  │               Texto               │
  ├───────────────────────────────────┤
  │ Tasa con 20% de descuento         │
  ├───────────────────────────────────┤
  │ Disponible 365 días al año        │
  ├───────────────────────────────────┤
  │ Aprobación por visador habilitado │
  ├───────────────────────────────────┤
  │ Documentación 100% digital        │
  └───────────────────────────────────┘

  Configuración del widget Icon List:
  - Ícono: Circle Check (o cualquier check de la librería)
  - Style → Icon: color #ffffff, background #2a9e2a, tamaño 22px, border-radius
  50%
  - Style → Text: color rgba(255,255,255,0.85), 14.5px
  - Style → Space Between: 14px
  - Style → Icon Spacing: 10px

  ---
  4. Botón CTA

  Widget Button:
  - Texto: Acceder al sistema
  - Link: URL del sistema de visado, abrir en nueva pestaña
  - Style → Background: #2a9e2a
  - Style → Border Radius: 6px
  - Style → Typography: Lato, 15px, 700
  - Style → Color: #ffffff
  - Style → Padding: 13px top/bottom, 24px left/right
  - Style → Box Shadow: 0 4px 16px rgba(42,158,42,0.4)
  - Style → Hover Background: #1f7a1f
  - Margin top: 8px

  ---
  Resultado esperado

  ┌─────────────────────────────────────────────────┐
  │ [gradiente azul #0d2d5e → #1a4a8a]              │
  │                                                  │
  │  SISTEMA ONLINE          ✓ Tasa con 20% dto      │
  │  Visado de trabajos      ✓ Disponible 365 días   │
  │  profesionales           ✓ Aprobación habilitada │
  │  100% online             ✓ Documentación digital │
  │                                                  │
  │  Realizá el visado...    [Acceder al sistema →]  │
  └─────────────────────────────────────────────────┘

  Sección completamente estática, sin plugins extra necesarios. La siguiente es
  Capacitación — lista de cursos sobre fondo gris #f0f2f7.

✻ Cogitated for 24s

※ recap: Estás construyendo la home de CIPBA en WordPress con Elementor Free y Astra Free. Terminaste el Banner de Visado; el próximo paso es armar la sección Capacitación (lista de cursos sobre fondo gris #f0f2f7).

❯ sigamos con la seccion "Próximos cursos"                                      

● Ya tengo el inicio, déjame leer el resto de la sección.

  Read 1 file (ctrl+o to expand)

● Tengo todo lo que necesito.

  ---
  Sección "Próximos Cursos" — Elementor Free

  Estructura visual

  Lista vertical de rows, cada uno con: ícono + título + fecha/modalidad a la
  izquierda, vacantes + botón a la derecha. Fondo #f0f2f7.

  ---
  Decisión: ¿estático o dinámico?

  Igual que con Noticias, los cursos deberían ser dinámicos (Custom Post Type).
  Sin embargo, con Elementor Free + EA Free el CPT con Post Grid tiene menos
  opciones de diseño que las noticias.

  Recomendación para esta sección: hacerla estática por ahora con widgets de
  Elementor. El layout de fila horizontal es difícil de lograr con Post Grid. Se
   puede migrar a dinámico después con un plugin más específico.

  ---
  1. Configurar la sección

  - Layout → Content Width: Boxed, 1200px
  - Layout → Padding: 60px top/bottom, 24px left/right
  - Style → Background Color: #f0f2f7

  ---
  2. Header de la sección

  Misma estructura que Noticias — dos columnas:

  Columna izquierda:
  - Widget Heading: FORMACIÓN PROFESIONAL — Lato, 12px, 700, uppercase,
  letter-spacing 2px, color #2a9e2a, margin-bottom 8px
  - Widget Heading: Próximos cursos — Roboto Condensed, clamp(22px,3vw,30px),
  900, color #0d2d5e

  Columna derecha (alineada al fondo):
  - Widget Button o texto: Ver toda la oferta →, color #2563b0, 14px, 600

  ---
  3. Cada fila de curso

  Cada curso es una Inner Section (2 columnas: 70% izquierda / 30% derecha) con:

  Configuración del contenedor de cada curso:
  - Background: #ffffff
  - Border: 1px solid #e8f1fc
  - Border radius: 10px
  - Padding: 20px top/bottom, 24px left/right
  - Box shadow: 0 2px 8px rgba(0,0,0,0.04)
  - Margin bottom: 14px
  - Hover en CSS:

  .curso-row:hover {
    box-shadow: 0 6px 20px rgba(0,0,0,0.09);
  }

  Agregá la clase CSS curso-row en Advanced → CSS Classes de cada inner section.

  ---
  Columna izquierda de cada curso (ícono + info)

  Usá una Inner Section de 2 columnas chicas:

  Sub-columna ícono:
  - Widget Icon: book/open-book de la librería Elementor
  - Tamaño: 22px, color #2563b0
  - Contenedor: 44×44px, background #e8f1fc, border-radius 8px
  - En Advanced → Custom CSS:
  selector {
    width: 44px;
    height: 44px;
    border-radius: 8px;
    background: #e8f1fc;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  Sub-columna texto:
  - Widget Heading: título del curso — 15px, 800, color #1a2540
  - Widget Text Editor: fecha — 12.5px, color #6b7a99 (con ícono calendar inline
   si querés)
  - Widget Heading (o Text): badge modalidad

  Badge modalidad — en CSS adicional según clase:
  .badge-virtual {
    background: #e8f5ee;
    color: #1a7a3a;
    font-size: 11.5px;
    font-weight: 700;
    padding: 2px 10px;
    border-radius: 20px;
    display: inline-block;
  }
  .badge-presencial {
    background: #e8f1fc;
    color: #2563b0;
    font-size: 11.5px;
    font-weight: 700;
    padding: 2px 10px;
    border-radius: 20px;
    display: inline-block;
  }

  ---
  Columna derecha de cada curso (vacantes + botón)

  Widget Heading — número de vacantes:
  - Texto: 12 / 8 / 25
  - 20px, 900
  - Color: vacantes < 10 → #e67e22 (naranja), ≥ 10 → #1a8a4a (verde)

  Widget Text debajo: vacantes — 11px, #9aa5b8

  Widget Button — Inscribirse:
  - Background: #0d2d5e
  - Hover: #1a4a8a
  - Border radius: 6px
  - Typography: 13.5px, 700
  - Padding: 10px top/bottom, 20px left/right
  - Color texto: blanco

  ---
  Datos de los 3 cursos

  ┌──────────────────────────────────┬────────────┬──────────────┬──────────┐
  │              Título              │ Modalidad  │    Fecha     │ Vacantes │
  ├──────────────────────────────────┼────────────┼──────────────┼──────────┤
  │ Integración y Automatización     │ Presencial │ Inicia 5     │ 12       │
  │ Profesional                      │            │ Mayo 2026    │          │
  ├──────────────────────────────────┼────────────┼──────────────┼──────────┤
  │ BIM – Building Information       │ Presencial │ Inicia 16    │ 8        │
  │ Modeling Módulo 1                │            │ Mayo 2026    │          │
  ├──────────────────────────────────┼────────────┼──────────────┼──────────┤
  │ Honorarios Mínimos: cálculo y    │ Virtual    │ Inicia 22    │ 25       │
  │ defensa profesional              │            │ Mayo 2026    │          │
  └──────────────────────────────────┴────────────┴──────────────┴──────────┘

  ---
  La siguiente sección es Institucional — grid de 2 columnas con texto/links a
  la izquierda y cards de sedes a la derecha.

✻ Sautéed for 30s

❯ necesito que esta seccion sea dinamica                                        

● La forma más limpia es: CPT "Curso" + ACF Free para los campos + shortcode PHP
   para el output. Todo con plugins gratuitos.

  ---
  Stack necesario

  ┌───────────────────────────────────┬───────────────────────────────────┐
  │              Plugin               │             Para qué              │
  ├───────────────────────────────────┼───────────────────────────────────┤
  │ Code Snippets (ya lo tenés)       │ Registrar el CPT + el shortcode   │
  ├───────────────────────────────────┼───────────────────────────────────┤
  │ Advanced Custom Fields (ACF) Free │ UI para los campos personalizados │
  └───────────────────────────────────┴───────────────────────────────────┘

  ---
  Paso 1 — Registrar el CPT

  En Code Snippets → Agregar nuevo, tipo PHP, ejecutar siempre:

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

  ---
  Paso 2 — Crear los campos en ACF

  ACF → Field Groups → Add New, asignar a Post Type = curso:

  ┌─────────────────┬──────────────────┬────────────────────────────────────┐
  │   Field Label   │    Field Name    │                Tipo                │
  ├─────────────────┼──────────────────┼────────────────────────────────────┤
  │ Modalidad       │ modalidad        │ Select → opciones: Presencial /    │
  │                 │                  │ Virtual                            │
  ├─────────────────┼──────────────────┼────────────────────────────────────┤
  │ Fecha           │ fecha            │ Text (ej: "Inicia 5 Mayo 2026")    │
  ├─────────────────┼──────────────────┼────────────────────────────────────┤
  │ Vacantes        │ vacantes         │ Number                             │
  ├─────────────────┼──────────────────┼────────────────────────────────────┤
  │ Link            │ link_inscripcion │ URL                                │
  │ inscripción     │                  │                                    │
  └─────────────────┴──────────────────┴────────────────────────────────────┘

  ---
  Paso 3 — Shortcode de display

  Nuevo snippet PHP en Code Snippets:

  add_shortcode('cursos_cipba', function () {
      $query = new WP_Query([
          'post_type'      => 'curso',
          'posts_per_page' => -1,
          'post_status'    => 'publish',
          'orderby'        => 'menu_order date',
          'order'          => 'ASC',
      ]);

      if (!$query->have_posts()) return '';

      ob_start();
      while ($query->have_posts()) {
          $query->the_post();
          $modalidad = get_field('modalidad');
          $fecha     = get_field('fecha');
          $vacantes  = (int) get_field('vacantes');
          $link      = get_field('link_inscripcion');

          $badge_class    = $modalidad === 'Virtual' ? 'cipba-badge-virtual' :
  'cipba-badge-presencial';
          $vacantes_color = $vacantes > 0 && $vacantes < 10 ? '#e67e22' :
  '#1a8a4a';
          ?>
          <div class="cipba-curso-row">
              <div class="cipba-curso-left">
                  <div class="cipba-curso-icon">
                      <svg width="22" height="22" viewBox="0 0 24 24"
  fill="none" stroke="#2563b0" stroke-width="2" stroke-linecap="round"
  stroke-linejoin="round">
                          <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/>
                          <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
                      </svg>
                  </div>
                  <div class="cipba-curso-info">
                      <div class="cipba-curso-titulo"><?php the_title();
  ?></div>
                      <div class="cipba-curso-meta">
                          <?php if ($fecha): ?>
                          <span class="cipba-curso-fecha">
                              <svg width="13" height="13" viewBox="0 0 24 24"
  fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round">
                                  <rect x="3" y="4" width="18" height="18"
  rx="2"/>
                                  <line x1="16" y1="2" x2="16" y2="6"/>
                                  <line x1="8" y1="2" x2="8" y2="6"/>
                                  <line x1="3" y1="10" x2="21" y2="10"/>
                              </svg>
                              <?php echo esc_html($fecha); ?>
                          </span>
                          <?php endif; ?>
                          <?php if ($modalidad): ?>
                          <span class="cipba-badge <?php echo
  esc_attr($badge_class); ?>">
                              <?php echo esc_html($modalidad); ?>
                          </span>
                          <?php endif; ?>
                      </div>
                  </div>
              </div>
              <div class="cipba-curso-right">
                  <?php if ($vacantes): ?>
                  <div class="cipba-vacantes">
                      <span class="cipba-vacantes-num" style="color:<?php echo
  esc_attr($vacantes_color); ?>">
                          <?php echo $vacantes; ?>
                      </span>
                      <span class="cipba-vacantes-label">vacantes</span>
                  </div>
                  <?php endif; ?>
                  <a href="<?php echo esc_url($link ?: '#'); ?>"
                     class="cipba-btn-inscribirse"
                     <?php echo $link ? 'target="_blank" rel="noopener"' : '';
  ?>>
                      Inscribirse
                  </a>
              </div>
          </div>
          <?php
      }
      wp_reset_postdata();
      return ob_get_clean();
  });

  ---
  Paso 4 — CSS en Apariencia → Personalizar → CSS adicional

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

  .cipba-curso-left { display: flex; align-items: center; gap: 16px; flex: 1;
  min-width: 240px; }

  .cipba-curso-icon {
      width: 44px; height: 44px; border-radius: 8px;
      background: #e8f1fc; display: flex;
      align-items: center; justify-content: center; flex-shrink: 0;
  }

  .cipba-curso-titulo { font-weight: 800; font-size: 15px; color: #1a2540;
  margin-bottom: 4px; }

  .cipba-curso-meta { display: flex; gap: 14px; flex-wrap: wrap; align-items:
  center; }

  .cipba-curso-fecha { font-size: 12.5px; color: #6b7a99; display: flex;
  align-items: center; gap: 4px; }

  .cipba-badge { font-size: 11.5px; font-weight: 700; padding: 2px 10px;
  border-radius: 20px; }
  .cipba-badge-virtual    { background: #e8f5ee; color: #1a7a3a; }
  .cipba-badge-presencial { background: #e8f1fc; color: #2563b0; }

  .cipba-curso-right { display: flex; align-items: center; gap: 20px; }

  .cipba-vacantes { text-align: center; }
  .cipba-vacantes-num   { display: block; font-size: 20px; font-weight: 900; }
  .cipba-vacantes-label { display: block; font-size: 11px; color: #9aa5b8; }

  .cipba-btn-inscribirse {
      background: #0d2d5e; color: #fff;
      padding: 10px 20px; border-radius: 6px;
      font-weight: 700; font-size: 13.5px;
      text-decoration: none; white-space: nowrap;
      transition: background 0.2s; display: inline-block;
  }
  .cipba-btn-inscribirse:hover { background: #1a4a8a; color: #fff; }

  ---
  Paso 5 — Elementor

  En la sección de Capacitación, dentro de la columna principal agregá un widget
   Shortcode con:

  [cursos_cipba]

  ---
  Flujo para el cliente

  Para agregar o editar un curso: Cursos → Agregar Nuevo → completar título + 4
  campos ACF → Publicar. Aparece automáticamente en la home.

✻ Baked for 57s

※ recap: Estás construyendo la home de CIPBA en WordPress con Elementor Free y Astra Free, siguiendo el prototipo del index.html. Terminaste el banner de Visado y la sección Próximos Cursos dinámica. El próximo paso es la sección Institucional.

❯ /rename wpplan 
  ⎿  Session renamed to: wpplan

❯ Unknown command: /expor. Did you mean /export?                                

● Args from unknown skill: wpplan-chat.md