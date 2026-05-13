# Sección 10 — Contacto: instrucciones WordPress

**Stack**: Elementor Free + Astra Free + **Contact Form 7** (plugin gratuito para el formulario).

**Estrategia CSS**: `<style>` dentro del widget HTML para estilos locales y hover, CSS Adicional para estilos compartidos y los estilos del formulario CF7.

---

## Plugin de formulario: Contact Form 7

Instalar desde **Plugins → Añadir nuevo** → buscar **"Contact Form 7"** → Instalar y activar. Es el plugin de formularios más usado en WordPress, 100% gratuito y sin limitaciones de campos.

---

## Estructura general

```
[Section — fondo #f0f2f7]
  [Header centrado]
    Eyebrow "Escribinos"
    H2 "Contacto"
  [Inner Section: 2 columnas ~42% | ~58%]
    [Columna izquierda]       [Columna derecha]
      Card Área Administrativa   Shortcode CF7 (formulario)
      Card Área Técnica
      Botón WhatsApp
```

---

## Paso 1 — Crear el formulario en Contact Form 7

Ir a **Contacto → Añadir nuevo** y crear el formulario con este template:

```
<div class="cf7-field-group">
  <label class="cf7-label">Nombre completo <span class="required">*</span></label>
  [text* nombre placeholder "Ing. Juan Pérez" class:cf7-input]
</div>

<div class="cf7-field-group">
  <label class="cf7-label">Correo electrónico <span class="required">*</span></label>
  [email* email placeholder "correo@ejemplo.com" class:cf7-input]
</div>

<div class="cf7-field-group">
  <label class="cf7-label">Asunto</label>
  [text asunto placeholder "Consulta sobre matrícula..." class:cf7-input]
</div>

<div class="cf7-field-group">
  <label class="cf7-label">Mensaje <span class="required">*</span></label>
  [textarea* mensaje placeholder "Tu consulta..." class:cf7-textarea]
</div>

[submit class:cf7-submit "Enviar mensaje"]
```

En la pestaña **Mail**, configurar:
- **Para**: `info@cipba.org`
- **Asunto**: `[asunto]`
- **Cuerpo**: `Nombre: [nombre]` / `Email: [email]` / `Mensaje: [mensaje]`

Guardar y copiar el shortcode generado, que tiene la forma `[contact-form-7 id="xxx" title="Contacto"]`.

---

## Paso 2 — Crear la sección en Elementor

### 2a. Section principal

1. Agregar **Section** con layout **1 columna** (para el header centrado).
2. En `Layout`:
   - **Stretch Section**: ON
   - **Content Width**: Boxed, `1200px`
   - **Padding**: `60px 24px`
3. En `Style` → **Background Color**: `#f0f2f7`
4. En `Advanced → CSS ID`: `contacto`

### 2b. Header centrado

Dentro de la columna única, agregar dos widgets:

**Widget Heading — Eyebrow**:
- Texto: `Escribinos`
- Tag: `P`
- Style: Color `#2a9e2a`, Lato `12px`, weight `700`, letter spacing `2px`, uppercase
- Margin bottom: `10px`
- Alineación: center

**Widget Heading — H2**:
- Texto: `Contacto`
- Tag: `H2`
- Style: Color `#0d2d5e`, tamaños Desktop `30px` / Tablet `26px` / Mobile `22px`, weight `900`
- Alineación: center
- Margin bottom: `40px`
- `Advanced → CSS Classes`: `contacto-h2`

### 2c. Inner Section con 2 columnas

Agregar un widget **Inner Section** debajo del header:
- Columna izquierda: **42%** de ancho
- Columna derecha: **58%** de ancho
- Column Gap: `40px`

---

## Paso 3 — Columna izquierda

### 3a. Card Área Administrativa

Widget **HTML** — incluye el `<style>` con todas las clases de las cards:

```html
<style>
.contacto-card {
  background: white;
  border-radius: 10px;
  padding: 24px;
  border: 1px solid #e8f1fc;
  margin-bottom: 16px;
}
.contacto-card-title {
  font-weight: 800;
  color: #0d2d5e;
  font-size: 15px;
  margin-bottom: 16px;
  font-family: 'Lato', sans-serif;
}
.contacto-card-items {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.contacto-card-item {
  font-size: 14px;
  color: #6b7a99;
  font-family: 'Lato', sans-serif;
  line-height: 1.4;
}
.contacto-card-item b {
  color: #3d4b63;
  font-weight: 700;
}
</style>

<div class="contacto-card">
  <div class="contacto-card-title">Área Administrativa</div>
  <div class="contacto-card-items">
    <div class="contacto-card-item"><b>Rolando Menna:</b> (011) 1158570060</div>
    <div class="contacto-card-item"><b>Griselda Bezerra:</b> (011) 1127134055</div>
    <div class="contacto-card-item"><b>Mónica Rodríguez:</b> (011) 1127133321</div>
  </div>
</div>
```

### 3b. Card Área Técnica

Widget **HTML** — reutiliza las clases del widget anterior (ya cargadas en página):

```html
<div class="contacto-card">
  <div class="contacto-card-title">Área Técnica</div>
  <div class="contacto-card-items">
    <div class="contacto-card-item"><b>Ing. Marcelo Romano:</b> (011) 1138293041</div>
    <div class="contacto-card-item"><b>Visador Ing. Pappolla:</b> (011) 1127133789</div>
  </div>
</div>
```

### 3c. Botón WhatsApp

Widget **HTML**:

```html
<style>
.wa-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  background: #25d366;
  color: white;
  padding: 14px 20px;
  border-radius: 8px;
  font-weight: 700;
  font-size: 15px;
  font-family: 'Lato', sans-serif;
  text-decoration: none;
  transition: background 0.2s;
}
.wa-btn:hover {
  background: #1da851;
  color: white;
}
</style>

<a href="https://wa.me/541138293041" target="_blank" rel="noopener" class="wa-btn">
  <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="white">
    <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/>
    <path d="M12 0C5.373 0 0 5.373 0 12c0 2.127.558 4.122 1.532 5.855L.057 23.882a.5.5 0 0 0 .61.61l6.05-1.484A11.945 11.945 0 0 0 12 24c6.627 0 12-5.373 12-12S18.627 0 12 0zm0 22c-1.907 0-3.693-.523-5.222-1.432l-.374-.22-3.88.952.98-3.774-.242-.389A9.96 9.96 0 0 1 2 12C2 6.477 6.477 2 12 2s10 4.477 10 10-4.477 10-10 10z"/>
  </svg>
  Consultar por WhatsApp
</a>
```

---

## Paso 4 — Columna derecha: formulario

Widget **Shortcode** (disponible en Elementor Free):
- Pegar el shortcode copiado de CF7: `[contact-form-7 id="xxx" title="Contacto"]`

El formulario aparece funcional. Los estilos del paso siguiente lo hacen coincidir con el diseño.

---

## Paso 5 — CSS Adicional completo para la sección

En **Apariencia → Personalizar → CSS Adicional**:

```css
/* === Sección Contacto === */

/* H2 tipografía */
.contacto-h2 .elementor-heading-title {
  font-family: 'Roboto Condensed', sans-serif;
}

/* Contenedor del formulario CF7 */
.wpcf7 {
  background: white;
  border-radius: 10px;
  padding: 32px;
  border: 1px solid #e8f1fc;
}

/* Labels */
.cf7-label {
  display: block;
  font-size: 13.5px;
  font-weight: 700;
  color: #3d4b63;
  margin-bottom: 6px;
  font-family: 'Lato', sans-serif;
}
.cf7-label .required {
  color: #c0392b;
  margin-left: 2px;
}

/* Inputs y textarea */
.cf7-input,
.cf7-textarea {
  width: 100%;
  padding: 10px 14px;
  border-radius: 6px;
  border: 1.5px solid #e0e6f0;
  font-size: 14px;
  font-family: 'Lato', sans-serif;
  outline: none;
  transition: border-color 0.2s;
  box-sizing: border-box;
  color: #1a2540;
}
.cf7-input:focus,
.cf7-textarea:focus {
  border-color: #2563b0;
}
.cf7-textarea {
  resize: vertical;
  min-height: 110px;
}

/* Errores de validación */
.wpcf7-not-valid-tip {
  color: #c0392b;
  font-size: 12px;
  margin-top: 4px;
  font-family: 'Lato', sans-serif;
}
.wpcf7-not-valid.cf7-input,
.wpcf7-not-valid.cf7-textarea {
  border-color: #c0392b;
}

/* Botón submit */
.cf7-submit {
  width: 100%;
  background: #0d2d5e;
  color: white;
  padding: 13px;
  border-radius: 6px;
  font-weight: 700;
  font-size: 15px;
  font-family: 'Lato', sans-serif;
  border: none;
  cursor: pointer;
  transition: background 0.2s;
  margin-top: 4px;
}
.cf7-submit:hover {
  background: #1a4a8a;
}

/* Mensaje de éxito */
.wpcf7-response-output {
  border: none !important;
  border-radius: 10px;
  padding: 48px 32px !important;
  text-align: center;
  background: white;
  margin: 0 !important;
  font-family: 'Lato', sans-serif;
}
.wpcf7-mail-sent-ok {
  color: #0d2d5e !important;
  font-size: 16px;
  font-weight: 700;
}

/* Mensaje de error global */
.wpcf7-mail-sent-ng,
.wpcf7-spam-blocked {
  color: #c0392b !important;
  background: #fef2f2;
  font-family: 'Lato', sans-serif;
}

/* Responsive: apilar columnas en ≤900px */
@media (max-width: 900px) {
  #contacto .elementor-inner-section .elementor-column {
    width: 100% !important;
  }
}
```

---

## Paso 6 — Estado de éxito mejorado (opcional)

El estado de éxito del prototipo muestra un ícono check verde con círculo. CF7 solo muestra texto plano. Para agregar el ícono, en la pestaña **Additional Settings** del formulario CF7 agregar:

```
on_sent_ok: "document.querySelector('.wpcf7-response-output').innerHTML = '<div style=\"width:64px;height:64px;border-radius:50%;background:#e8f5ee;display:flex;align-items:center;justify-content:center;margin:0 auto 20px\"><svg width=\"28\" height=\"28\" viewBox=\"0 0 28 28\"><polyline points=\"4,14 10,20 24,8\" stroke=\"#1a8a4a\" stroke-width=\"2.5\" fill=\"none\" stroke-linecap=\"round\"/></svg></div><h3 style=\"color:#0d2d5e;font-size:20px;font-weight:800;margin-bottom:10px\">¡Mensaje enviado!</h3><p style=\"color:#6b7a99\">Nos pondremos en contacto a la brevedad. Muchas gracias.</p>';"
```

---

## Resumen de widgets y plugins

| Elemento | Solución |
|---|---|
| Formulario | Contact Form 7 (free) + widget Shortcode de Elementor |
| Cards de info | Widget HTML con `<style>` embebido |
| Botón WhatsApp | Widget HTML con `<style>` embebido |
| Estilos CF7 | CSS Adicional (inputs, labels, botón, errores, éxito) |
| Responsive | CSS Adicional + ajuste manual en vista Tablet de Elementor |

**Sin widgets Pro. Sin plugins de pago.**
