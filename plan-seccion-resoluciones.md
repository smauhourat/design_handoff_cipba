# Plan: Sección Normativa (Reglamentaciones y Resoluciones)

## Contexto
Implementar la sección 8 del diseño CIPBA (README2.md / index2.html) en WordPress con Elementor Free + Astra Free + Code Snippets + ACF Free + PDF Embedder (ya instalado). La sección es interactiva: búsqueda en vivo, filtros por categoría (chips), lista de documentos con filas expandibles que muestran una preview del PDF embebido + panel de metadatos.

---

## Stack de implementación
- **Code Snippets**: CPT + taxonomy + shortcode PHP + JS
- **ACF Free**: campos personalizados por documento
- **PDF Embedder** (instalado): viewer del PDF en el panel de preview
- **Elementor Free**: widget Shortcode para embeber la sección
- **Apariencia → CSS adicional**: estilos

---

## Paso 1 — CPT `resoluciones` + Taxonomy `cat_normativa`

**Snippet PHP nuevo en Code Snippets** (ejecutar siempre):

```php
// CPT Resoluciones
add_action('init', function () {
    register_post_type('resolucion', [
        'labels'       => ['name' => 'Resoluciones', 'singular_name' => 'Resolución', 'add_new_item' => 'Agregar Resolución', 'edit_item' => 'Editar Resolución'],
        'public'       => true,
        'show_in_menu' => true,
        'supports'     => ['title'],
        'menu_icon'    => 'dashicons-media-document',
        'has_archive'  => false,
    ]);

    register_taxonomy('cat_normativa', 'resolucion', [
        'labels'       => ['name' => 'Categorías', 'singular_name' => 'Categoría', 'add_new_item' => 'Nueva Categoría'],
        'hierarchical' => true,
        'show_ui'      => true,
        'rewrite'      => ['slug' => 'categoria-normativa'],
    ]);
});
```

---

## Paso 2 — Campos ACF

**ACF → Field Groups → Add New**, asignar a Post Type = `resolucion`:

| Label | Field Name | Tipo | Notas |
|-------|------------|------|-------|
| Número | `numero` | Text | Ej: "CS 187/2026" |
| Tipo | `tipo` | Select | Opciones: Resolución / Reglamento / Disposición |
| Fecha | `fecha` | Text | Ej: "02 Abr 2026" |
| Archivo PDF | `archivo_pdf` | File | Return Value: File URL |
| Páginas | `paginas` | Number | |
| Tamaño | `tamanio` | Text | Ej: "342 KB" |
| Estado | `estado` | Select | Opciones: Vigente / Derogado / Suspendido. Default: Vigente |

---

## Paso 3 — Crear términos de taxonomy

En **Resoluciones → Categorías**, crear los 5 términos:
- Honorarios
- Visado
- Institucional
- Matrícula
- Capacitación

---

## Paso 4 — Shortcode PHP

**Snippet PHP nuevo en Code Snippets**:

```php
add_shortcode('normativa_cipba', function () {

    // Colores por categoría (hardcoded, coinciden con el diseño)
    $cat_colors = [
        'honorarios'   => '#8a1a1a',
        'visado'       => '#2563b0',
        'institucional'=> '#0d2d5e',
        'matricula'    => '#1a8a4a',
        'capacitacion' => '#7a1a8a',
    ];

    // Obtener todos los términos activos
    $terms = get_terms(['taxonomy' => 'cat_normativa', 'hide_empty' => true]);

    // Query de documentos
    $query = new WP_Query([
        'post_type'      => 'resolucion',
        'posts_per_page' => -1,
        'post_status'    => 'publish',
        'orderby'        => 'date',
        'order'          => 'DESC',
    ]);

    if (!$query->have_posts()) return '<p style="text-align:center;color:#9aa5b8">No hay documentos publicados.</p>';

    // Construir array de docs para data attributes (para el JS de filtrado)
    $docs = [];
    while ($query->have_posts()) {
        $query->the_post();
        $term_objs  = wp_get_post_terms(get_the_ID(), 'cat_normativa');
        $term_slug  = !empty($term_objs) ? $term_objs[0]->slug : '';
        $term_name  = !empty($term_objs) ? $term_objs[0]->name : '';
        $color      = $cat_colors[$term_slug] ?? '#2563b0';
        $pdf_url    = get_field('archivo_pdf');

        $docs[] = [
            'id'       => get_the_ID(),
            'titulo'   => get_the_title(),
            'numero'   => get_field('numero'),
            'tipo'     => get_field('tipo'),
            'fecha'    => get_field('fecha'),
            'paginas'  => get_field('paginas'),
            'tamanio'  => get_field('tamanio'),
            'estado'   => get_field('estado') ?: 'Vigente',
            'cat_slug' => $term_slug,
            'cat_name' => $term_name,
            'color'    => $color,
            'pdf_url'  => $pdf_url,
        ];
    }
    wp_reset_postdata();

    ob_start();
    ?>
    <div class="cipba-normativa-wrap">

        <!-- HEADER -->
        <div class="cipba-norm-header">
            <div>
                <p class="cipba-eyebrow">Marco normativo</p>
                <h2 class="cipba-norm-title">Reglamentaciones y Resoluciones</h2>
                <p class="cipba-norm-desc">Accedé al archivo oficial de resoluciones, reglamentos y disposiciones del Distrito VII y del Consejo Superior.</p>
            </div>
            <a href="#" class="cipba-archive-link">Archivo histórico completo ›</a>
        </div>

        <!-- TOOLBAR -->
        <div class="cipba-norm-toolbar">
            <div class="cipba-search-wrap">
                <svg class="cipba-search-icon" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
                <input id="cipba-norm-search" type="text" placeholder="Buscar por título o número..." class="cipba-search-input" autocomplete="off">
            </div>
            <div class="cipba-chips-wrap">
                <button class="cipba-chip cipba-chip-active" data-cat="todas">Todas</button>
                <?php foreach ($terms as $term): ?>
                    <button class="cipba-chip" data-cat="<?php echo esc_attr($term->slug); ?>">
                        <?php echo esc_html($term->name); ?>
                    </button>
                <?php endforeach; ?>
            </div>
        </div>

        <!-- CONTADOR -->
        <div id="cipba-norm-counter" class="cipba-norm-counter"></div>

        <!-- LISTA -->
        <div class="cipba-norm-list" id="cipba-norm-list">
            <?php foreach ($docs as $i => $doc):
                $color      = $doc['color'];
                $pdf_url    = $doc['pdf_url'];
                $is_last    = ($i === count($docs) - 1);
                $embed_code = $pdf_url ? do_shortcode('[pdf-embedder url="' . esc_url($pdf_url) . '" title="' . esc_attr($doc['titulo']) . '"]') : '';
            ?>
            <div class="cipba-norm-row<?php echo $is_last ? ' cipba-last' : ''; ?>"
                 data-cat="<?php echo esc_attr($doc['cat_slug']); ?>"
                 data-titulo="<?php echo esc_attr(strtolower($doc['titulo'])); ?>"
                 data-numero="<?php echo esc_attr(strtolower($doc['numero'])); ?>">

                <!-- FILA PRINCIPAL -->
                <div class="cipba-norm-grid">

                    <!-- Icono PDF -->
                    <div class="cipba-pdf-icon" style="background:<?php echo esc_attr($color); ?>18;border-color:<?php echo esc_attr($color); ?>28">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="<?php echo esc_attr($color); ?>" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/><polyline points="10 9 9 9 8 9"/></svg>
                        <span class="cipba-pdf-label" style="color:<?php echo esc_attr($color); ?>">PDF</span>
                    </div>

                    <!-- Título y meta -->
                    <div class="cipba-norm-info">
                        <div class="cipba-norm-badges">
                            <span class="cipba-cat-badge" style="background:<?php echo esc_attr($color); ?>20;color:<?php echo esc_attr($color); ?>"><?php echo esc_html($doc['cat_name']); ?></span>
                            <span class="cipba-norm-num"><?php echo esc_html($doc['tipo'] . ' ' . $doc['numero']); ?></span>
                        </div>
                        <div class="cipba-norm-doc-titulo"><?php echo esc_html($doc['titulo']); ?></div>
                    </div>

                    <!-- Fecha -->
                    <div class="cipba-norm-fecha reg-date">
                        <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="#9aa5b8" stroke-width="2" stroke-linecap="round"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
                        <?php echo esc_html($doc['fecha']); ?>
                    </div>

                    <!-- Tamaño -->
                    <div class="cipba-norm-size reg-size"><?php echo esc_html($doc['paginas'] . ' pág · ' . $doc['tamanio']); ?></div>

                    <!-- Acciones -->
                    <div class="cipba-norm-actions">
                        <?php if ($pdf_url): ?>
                        <button class="cipba-btn-ver" data-idx="<?php echo $i; ?>"
                                style="color:<?php echo esc_attr($color); ?>;border-color:<?php echo esc_attr($color); ?>"
                                data-color="<?php echo esc_attr($color); ?>">
                            <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/></svg>
                            Ver
                        </button>
                        <a href="<?php echo esc_url($pdf_url); ?>" class="cipba-btn-pdf" download target="_blank">
                            <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
                            PDF
                        </a>
                        <?php else: ?>
                        <span class="cipba-no-pdf">Sin archivo</span>
                        <?php endif; ?>
                    </div>
                </div>

                <!-- PREVIEW EXPANDIBLE -->
                <?php if ($pdf_url): ?>
                <div class="cipba-norm-preview" id="cipba-preview-<?php echo $i; ?>" style="display:none;border-top-color:<?php echo esc_attr($color); ?>40">
                    <div class="cipba-preview-grid">
                        <!-- PDF Embedder -->
                        <div class="cipba-preview-pdf">
                            <?php echo $embed_code; ?>
                        </div>
                        <!-- Metadatos -->
                        <div class="cipba-preview-meta">
                            <div class="cipba-meta-title">Información del documento</div>
                            <?php
                            $meta_rows = [
                                ['Tipo',      $doc['tipo']],
                                ['Número',    $doc['numero']],
                                ['Categoría', $doc['cat_name']],
                                ['Fecha',     $doc['fecha']],
                                ['Páginas',   $doc['paginas']],
                                ['Tamaño',    $doc['tamanio']],
                                ['Estado',    '✓ ' . $doc['estado']],
                            ];
                            foreach ($meta_rows as [$k, $v]):
                            ?>
                            <div class="cipba-meta-row">
                                <span class="cipba-meta-key"><?php echo esc_html($k); ?></span>
                                <span class="cipba-meta-val"><?php echo esc_html($v); ?></span>
                            </div>
                            <?php endforeach; ?>
                            <a href="<?php echo esc_url($pdf_url); ?>" class="cipba-btn-download" download target="_blank"
                               style="background:<?php echo esc_attr($color); ?>">
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
                                Descargar PDF completo
                            </a>
                        </div>
                    </div>
                </div>
                <?php endif; ?>
            </div>
            <?php endforeach; ?>

            <!-- EMPTY STATE -->
            <div class="cipba-empty-state" id="cipba-empty-state" style="display:none">
                No se encontraron documentos con esos criterios.
            </div>
        </div>
    </div>

    <script>
    (function(){
        var rows    = document.querySelectorAll('.cipba-norm-row');
        var chips   = document.querySelectorAll('.cipba-chip');
        var search  = document.getElementById('cipba-norm-search');
        var counter = document.getElementById('cipba-norm-counter');
        var empty   = document.getElementById('cipba-empty-state');
        var activeCat = 'todas';

        function updateCounter(count) {
            counter.textContent = count + (count === 1 ? ' documento' : ' documentos');
        }

        function filterRows() {
            var q   = search.value.toLowerCase().trim();
            var vis = 0;
            rows.forEach(function(row) {
                var catMatch   = activeCat === 'todas' || row.dataset.cat === activeCat;
                var searchMatch = !q || row.dataset.titulo.includes(q) || row.dataset.numero.includes(q);
                var show = catMatch && searchMatch;
                row.style.display = show ? '' : 'none';
                if (show) vis++;
            });
            updateCounter(vis);
            empty.style.display = vis === 0 ? 'block' : 'none';
        }

        // Chips
        chips.forEach(function(chip) {
            chip.addEventListener('click', function() {
                chips.forEach(function(c){ c.classList.remove('cipba-chip-active'); });
                chip.classList.add('cipba-chip-active');
                activeCat = chip.dataset.cat;
                filterRows();
            });
        });

        // Search
        search.addEventListener('input', filterRows);

        // Botones Ver (toggle preview)
        document.querySelectorAll('.cipba-btn-ver').forEach(function(btn) {
            btn.addEventListener('click', function() {
                var idx     = btn.dataset.idx;
                var preview = document.getElementById('cipba-preview-' + idx);
                var color   = btn.dataset.color;
                var isOpen  = preview.style.display !== 'none';

                // Cerrar todos los previews abiertos
                document.querySelectorAll('.cipba-norm-preview').forEach(function(p){ p.style.display = 'none'; });
                document.querySelectorAll('.cipba-btn-ver').forEach(function(b){
                    b.style.background = 'transparent';
                    b.style.color = b.dataset.color;
                    b.style.borderColor = b.dataset.color;
                });

                if (!isOpen) {
                    preview.style.display = 'block';
                    btn.style.background  = color;
                    btn.style.color       = 'white';
                    btn.style.borderColor = color;
                    // Scroll suave a la preview
                    preview.scrollIntoView({behavior: 'smooth', block: 'nearest'});
                }
            });
        });

        // Inicializar contador
        filterRows();
    })();
    </script>
    <?php
    return ob_get_clean();
});
```

---

## Paso 5 — CSS en Apariencia → CSS adicional

```css
/* ── NORMATIVA WRAPPER ─────────────────────── */
.cipba-normativa-wrap { max-width: 1200px; margin: 0 auto; }

/* Header */
.cipba-norm-header { display: flex; justify-content: space-between; align-items: flex-end; flex-wrap: wrap; gap: 12px; margin-bottom: 28px; }
.cipba-eyebrow { color: #2a9e2a; font-size: 12px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 8px; }
.cipba-norm-title { font-family: 'Roboto Condensed', sans-serif; font-size: clamp(22px, 3vw, 30px); font-weight: 900; color: #0d2d5e; margin-bottom: 8px; }
.cipba-norm-desc { color: #6b7a99; font-size: 14.5px; }
.cipba-archive-link { color: #2563b0; font-size: 14px; font-weight: 600; text-decoration: none; white-space: nowrap; }

/* Toolbar */
.cipba-norm-toolbar { display: flex; gap: 12px; flex-wrap: wrap; align-items: center; margin-bottom: 14px; }
.cipba-search-wrap { position: relative; flex: 1 1 260px; min-width: 200px; }
.cipba-search-icon { position: absolute; left: 11px; top: 50%; transform: translateY(-50%); pointer-events: none; }
.cipba-search-input { width: 100% !important; padding: 10px 14px 10px 36px !important; border-radius: 6px; border: 1.5px solid #e0e6f0 !important; background: #f8f9fc !important; font-size: 13.5px !important; color: #1a2540 !important; outline: none !important; box-sizing: border-box !important; }

.cipba-search-input:focus { border-color: #2563b0; }
.cipba-chips-wrap { display: flex; gap: 6px; flex-wrap: wrap; }
.cipba-chip { padding: 8px 14px; border-radius: 20px; border: 1.5px solid #e0e6f0; background: white; color: #6b7a99; font-size: 12.5px; font-weight: 700; cursor: pointer; transition: all 0.15s; }
.cipba-chip-active { border-color: #0d2d5e !important; background: #0d2d5e !important; color: white !important; }

/* Contador */
.cipba-norm-counter { font-size: 12.5px; color: #9aa5b8; margin-bottom: 14px; }

/* Lista */
.cipba-norm-list { border: 1px solid #e8f1fc; border-radius: 10px; overflow: hidden; background: white; }
.cipba-norm-row { border-bottom: 1px solid #e8f1fc; background: white; transition: background 0.15s; }
.cipba-norm-row.cipba-last { border-bottom: none; }
.cipba-norm-grid { display: grid; grid-template-columns: 52px 1fr auto auto auto; gap: 16px; align-items: center; padding: 16px 20px; }

/* Icono PDF */
.cipba-pdf-icon { width: 44px; height: 52px; border-radius: 4px; border: 1px solid; display: flex; flex-direction: column; align-items: center; justify-content: center; flex-shrink: 0; }
.cipba-pdf-label { font-size: 8.5px; font-weight: 800; margin-top: 2px; letter-spacing: 0.5px; }

/* Info */
.cipba-norm-badges { display: flex; align-items: center; gap: 8px; margin-bottom: 4px; flex-wrap: wrap; }
.cipba-cat-badge { font-size: 10.5px; font-weight: 800; padding: 2px 8px; border-radius: 3px; letter-spacing: 0.5px; text-transform: uppercase; }
.cipba-norm-num { font-family: 'Roboto Condensed', sans-serif; font-size: 11.5px; color: #9aa5b8; font-weight: 700; letter-spacing: 0.5px; }
.cipba-norm-doc-titulo { font-size: 14.5px; font-weight: 700; color: #1a2540; line-height: 1.4; }

/* Fecha / Tamaño */
.cipba-norm-fecha { display: flex; align-items: center; gap: 6px; font-size: 13px; color: #6b7a99; white-space: nowrap; }
.cipba-norm-size { font-family: 'Roboto Condensed', sans-serif; font-size: 12px; color: #9aa5b8; letter-spacing: 0.3px; white-space: nowrap; }

/* Acciones */
.cipba-norm-actions { display: flex; gap: 6px; align-items: center; }
.cipba-btn-ver { padding: 8px 12px; border-radius: 5px; border: 1.5px solid; background: transparent; font-size: 12.5px; font-weight: 700; cursor: pointer; display: flex; align-items: center; gap: 5px; transition: all 0.15s; white-space: nowrap; }
.cipba-btn-pdf { padding: 8px 12px; border-radius: 5px; background: #0d2d5e; color: white; font-size: 12.5px; font-weight: 700; text-decoration: none; display: flex; align-items: center; gap: 5px; transition: background 0.15s; white-space: nowrap; }
.cipba-btn-pdf:hover { background: #1a4a8a; color: white; }
.cipba-no-pdf { font-size: 12px; color: #9aa5b8; }

/* Preview expandible */
.cipba-norm-preview { padding: 0 20px 24px; border-top: 1px dashed; }
.cipba-preview-grid { display: grid; grid-template-columns: 1fr 280px; gap: 20px; margin-top: 18px; }
.cipba-preview-pdf { min-height: 300px; }
.cipba-preview-meta { display: flex; flex-direction: column; gap: 10px; font-size: 13px; }
.cipba-meta-title { font-weight: 800; color: #0d2d5e; font-size: 13px; margin-bottom: 4px; }
.cipba-meta-row { display: flex; justify-content: space-between; padding: 6px 0; border-bottom: 1px dashed #e8f1fc; }
.cipba-meta-key { color: #9aa5b8; font-size: 12px; }
.cipba-meta-val { color: #3d4b63; font-weight: 700; font-size: 12.5px; }
.cipba-btn-download { margin-top: 6px; color: white; padding: 10px; border-radius: 5px; font-weight: 700; font-size: 13px; text-align: center; display: flex; align-items: center; justify-content: center; gap: 6px; text-decoration: none; transition: opacity 0.15s; }
.cipba-btn-download:hover { opacity: 0.88; color: white; }

/* Empty state */
.cipba-empty-state { padding: 48px 20px; text-align: center; color: #9aa5b8; font-size: 14px; }

/* Responsive */
@media (max-width: 768px) {
    .reg-date, .reg-size, .cipba-norm-fecha, .cipba-norm-size { display: none; }
    .cipba-norm-grid { grid-template-columns: 44px 1fr auto; }
    .cipba-preview-grid { grid-template-columns: 1fr; }
    .cipba-norm-header { flex-direction: column; align-items: flex-start; }
}
```

---

## Paso 6 — Sección en Elementor

1. Nueva sección debajo del Banner Visado
2. Background: `#ffffff`, padding 60px top/bottom, 24px left/right
3. Content width: Boxed 1200px
4. Widget **Shortcode**: `[normativa_cipba]`

---

## Paso 7 — Cargar documentos de prueba

En **Resoluciones → Agregar Nueva** con estos datos del prototipo:

| Título | Número | Tipo | Fecha | Categoría | Páginas | Tamaño |
|--------|--------|------|-------|-----------|---------|--------|
| Actualización del cuadro de honorarios mínimos – 1° trimestre 2026 | CS 187/2026 | Resolución | 02 Abr 2026 | Honorarios | 12 | 342 KB |
| Régimen de visado de trabajos profesionales – Modalidad online | CS 174/2026 | Resolución | 14 Mar 2026 | Visado | 18 | 486 KB |
| Reglamento interno de la Asamblea General Ordinaria del Distrito VII | D7 12/2026 | Reglamento | 28 Feb 2026 | Institucional | 8 | 215 KB |
| Cuota anual de matrícula y bonificaciones para el ejercicio 2026 | CS 158/2026 | Resolución | 15 Feb 2026 | Matrícula | 6 | 198 KB |

Para cada una: subir el PDF real en el campo **Archivo PDF**.

---

## Verificación

1. Ir al frontend de la home y verificar que aparece la sección
2. Escribir en el buscador → filas se filtran en tiempo real
3. Hacer click en un chip de categoría → se filtran por categoría
4. Hacer click en "Ver" → se expande el panel con el PDF Embedder + metadatos
5. Hacer click en "PDF" → descarga el archivo
6. Buscar algo que no existe → aparece "No se encontraron documentos..."
7. Verificar en mobile (768px) que fecha y tamaño se ocultan, y el preview pasa a 1 columna
