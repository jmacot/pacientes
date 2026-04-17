# Guía de estilo · Portal de Pacientes

> Referencia visual y técnica para añadir nuevas patologías, guías o secciones al portal. Hereda de `COT/STYLE-GUIDE.md` (Sistema A "Editorial") y sobrescribe lo necesario para el contexto del paciente.

---

## 1. Principios

1. **El paciente no es clínico.** Lenguaje directo, frases cortas, negritas para lo importante. Evitar jerga médica salvo explicación inmediata.
2. **Calma visual + toque generativo.** El portal debe transmitir profesionalidad y serenidad. El mesh gradient animado aporta el "toque humano" sin ser intrusivo.
3. **Continuidad con el hub.** El portal es una extensión de `jmacot.github.io` — mismas fuentes, mismos patrones, mismo mesh. Un paciente que venga de la landing no debe sentir corte.
4. **Sin dark mode.** Decisión consciente: identidad visual única y clara para contexto clínico. No reintroducir.

---

## 2. Variables CSS base

Copiar estas variables al `:root` de cualquier archivo nuevo:

```css
:root {
  --bg: #e8edf4;
  --surface: #ffffff;
  --ink: #0f172a;
  --ink-muted: #64748b;
  --border: #e2e8f0;

  /* Sombras — doble capa siempre, nunca capa única */
  --shadow-sm: 0 1px 3px 0 rgb(0 0 0 / 0.06), 0 1px 2px -1px rgb(0 0 0 / 0.06);
  --shadow: 0 4px 6px -1px rgb(0 0 0 / 0.08), 0 2px 4px -2px rgb(0 0 0 / 0.06);
  --shadow-hover: 0 25px 50px -12px rgb(0 0 0 / 0.15);

  --radius: 20px;
  --radius-lg: 24px;
  --transition-smooth: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);

  /* Paleta anatómica — namespace propio del portal */
  --c-rodilla: #0ea5e9;  --c-rodilla-light: #e0f2fe;
  --c-cadera:  #8b5cf6;  --c-cadera-light:  #ede9fe;
  --c-hombro:  #0d9488;  --c-hombro-light:  #ccfbf1;
  --c-columna: #f59e0b;  --c-columna-light: #fef3c7;
  --c-general: #64748b;  --c-general-light: #f1f5f9;

  /* Semánticas de estado */
  --green: #16a34a;      --green-light: #dcfce7;
  --red: #dc2626;        --red-light: #fef2f2;
  --amber: #d97706;      --amber-light: #fef3c7;
}
```

> **Regla:** al añadir una zona anatómica nueva, seguir el patrón `--c-{zona}` + `--c-{zona}-light`. Elegir un color claramente distinto de los existentes (contraste visual en filtros).

---

## 3. Tipografía

| Uso | Fuente | Peso | Tamaño |
|-----|--------|------|--------|
| Títulos (h1, h2 serif, card titles) | DM Serif Display | 400 | `clamp(2rem, 5vw, 3.2rem)` (h1 hero) · `1.4rem` (card) · `1.15rem` (section) |
| Cuerpo, párrafos | DM Sans | 300–500 | `14.5–15px` |
| Labels, pills, metadata, códigos | DM Mono | 400–500 | `10–12px` con `letter-spacing: 0.05–0.15em` + `text-transform: uppercase` |

Importar siempre este enlace único:

```html
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Mono:wght@400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
```

---

## 4. Fondo mesh gradient

**Solo en `index.html`** (landing). Los hubs y guías mantienen fondo sólido `var(--bg)` para no competir con el contenido denso.

Si en el futuro se quisiera aplicar a un hub nuevo, copiar el bloque `.mesh-bg` + 5 orbs + `@keyframes orb1–5` de `index.html:80-180` y los divs correspondientes al `<body>`. No olvidar `header, main, footer { position: relative; z-index: 1; }`.

Los colores de los orbs están sincronizados con `jmacot.github.io` (sky, violet, teal, amber, pink) — no cambiar salvo mesh específico por patología.

---

## 5. Arquitectura de páginas

| Tipo | Rol | Fondo | Nav sticky | Acordeones |
|------|-----|-------|------------|------------|
| `index.html` | Landing | Mesh animado | No | No |
| `{patologia}.html` (hub) | Selector info/rehab | Sólido | No | No |
| `{patologia}-info.html` | Guía información | Sólido | **Sí** (pills) | **Sí** (`<details>`) |
| `{patologia}-rehab.html` | Rehabilitación | Sólido | **Sí** (pills) | **Sí** (`<details>`) |
| `{tratamiento}.html` (enlace directo) | Guía sin hub | Sólido | Sí | Sí |

**Regla crítica:** las guías siguen las 8 secciones obligatorias del CLAUDE.md (Introducción, Hospital, Heparina, Recuperación, Expectativas, Claves, Alarma, FAQ). Ver `CLAUDE.md` sección 3.

---

## 6. Componentes

### 6.1. Header (páginas internas, no landing)

```css
header {
  background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
  color: white;
  padding: 56px 48px 48px;
  position: relative;
  overflow: hidden;
}
header::before, header::after {
  content: ''; position: absolute; border-radius: 50%; filter: blur(40px);
  /* ::before = glow sky arriba/derecha, ::after = glow violeta abajo/izquierda */
}
```

Contenido:
```html
<a class="back-home" href="{hub}.html" title="Volver">&larr; Volver</a>
<div class="header-label">Gu&iacute;a del paciente</div>
<h1>T&iacute;tulo<br><em>Subt&iacute;tulo</em></h1>
<p>Descripci&oacute;n breve en una o dos frases.</p>
```

En móvil: `header::before, header::after { display: none; }` (ahorra render).

### 6.2. Card (landing + hubs)

```css
.card {
  background: rgba(255,255,255,0.85);
  backdrop-filter: blur(12px);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 32px;
  box-shadow: var(--shadow);
  transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
  animation: fadeInUp 0.6s ease-out both;
}
.card:hover {
  transform: translateY(-6px);
  box-shadow: var(--shadow-hover);
  border-color: transparent;
}
.card::before {
  /* Accent line top: 3px de altura con color de la zona anatómica */
  content: ''; position: absolute; top: 0; left: 0; right: 0;
  height: 3px; background: var(--card-accent);
}
```

**Animación escalonada:** usar `nth-child` o `nth-of-type`:
```css
.card:nth-child(1) { animation-delay: 0.05s; }
.card:nth-child(2) { animation-delay: 0.15s; }
/* +0.10s por card */
```

El `backdrop-filter: blur(12px)` es deliberado en la landing (sobre mesh). En hubs con fondo sólido puede omitirse — `background: var(--surface)` es suficiente.

### 6.3. Sección-acordeón (guías)

```html
<details class="info-section" id="sec-intro" open>
  <summary>
    <span class="info-icon"><svg>...</svg></span>
    <span class="info-title">T&iacute;tulo</span>
    <svg class="info-chevron"><polyline points="6 9 12 15 18 9"/></svg>
  </summary>
  <div class="info-body">
    ...contenido...
  </div>
</details>
```

Primera sección (`sec-intro`) siempre lleva `open`. Resto cerradas.

**Iconos obligatorios por sección** (usar siempre los mismos):

| Sección | Icono (línea/trazo) | Concepto |
|---------|---------------------|----------|
| Introducción | círculo con `i` | información |
| Hospital | portapapeles | clínica |
| Heparina | jeringa | inyección |
| Recuperación | línea ascendente | progreso |
| Expectativas | gráfico de barras | datos |
| Claves | bocadillo de diálogo | mensaje |
| Alarma | triángulo con `!` | alerta |
| FAQ | signo de interrogación en círculo | preguntas |

### 6.4. Nav pills sticky (guías)

Botones scrollables horizontalmente con scroll spy. Ver `ptr-info.html` como referencia. Clase `.section-nav` con `position: sticky; top: 0; z-index: 50;` y `.nav-pill.active` con color de la zona anatómica.

### 6.5. Callouts

| Tipo | Uso | Clase |
|------|-----|-------|
| Informativo | Tips, notas, analogías | `.callout` (fondo sky light, borde sky) |
| Advertencia | Importante pero no urgente | `.alarm-callout` (fondo amber light, borde amber) |
| Peligro | Signos que requieren urgencias | `.alarm-callout.danger` (fondo red light, borde red) |
| Cierre | "Recuerda" al final de la guía | `.final-callout` (fondo sky light centrado) |

Patrón visual: borde izquierdo de 4px + padding generoso + fondo semitransparente.

### 6.6. Milestone cards (sección Recuperación)

Grid vertical con conector lateral:

```css
.milestones {
  display: grid; gap: 16px;
  /* ← línea conectora vertical entre cards */
}
.milestone-card {
  border-left: 4px solid var(--c-rodilla);
  background: var(--c-rodilla-light);
  padding: 18px 22px;
  border-radius: var(--radius-sm, 12px);
}
```

Cada milestone tiene un `milestone-label` (DM Mono, uppercase) con la ventana temporal ("0–6 semanas", "6 semanas – 3 meses") y una lista de hitos.

Si la milestone lleva imagen, usar layout `milestone-content` (flex horizontal, imagen a la derecha `width: 300px`). En móvil (`max-width: 600px`) apilar vertical.

### 6.7. Tabla comparativa "Expectativas vs realidad"

Dos columnas: mito (rojo suave) vs realidad (verde suave). En móvil se convierte en `.compare-mobile` apilado (una tarjeta por fila).

### 6.8. FAQ

Acordeones anidados dentro de la sección FAQ. Estructura `<details class="faq-item">` con summary minimalista (sin icono, sólo texto y chevron a la derecha). Fondo `var(--surface)`, borde ligero.

---

## 7. Imágenes

### 7.1. Organización

```
img/
├── logos/          → Logos institucionales
├── compartidas/    → Multi-guía (heparina, rodillera, ejercicios genéricos)
├── {patologia}/    → Específicas de la patología
├── _archivo/       → No usadas (base de retoque)
```

### 7.2. Clases

```css
.info-img { max-width: min(540px, 100%); margin: 0 auto; display: block; border-radius: 12px; }
.info-img.medium { max-width: min(420px, 100%); }
.info-img.small { max-width: min(280px, 100%); }
.info-img-caption { font-size: 12px; color: var(--ink-muted); text-align: center; margin-top: 8px; font-family: 'DM Mono', monospace; }
```

### 7.3. Recorte obligatorio

Antes de añadir una imagen, eliminar márgenes blancos con Pillow. Script en `CLAUDE.md` sección 3.

### 7.4. Alt text

Siempre descriptivo. Nunca dejar `alt=""` salvo imágenes puramente decorativas.

---

## 8. Animaciones

| Nombre | Uso | Duración |
|--------|-----|----------|
| `fadeInUp` | Entrada de cards, header | 0.6s `ease-out` |
| `pulse` | Dot verde "online" en header badge | 2s infinite |
| `orb1–5` | Mesh gradient de fondo | 18–24s infinite |

**Regla:** envolver siempre en:
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

Los hovers con `transform: translateY(-6px)` son obligatorios en cards. Sin hover, la página se siente muerta.

---

## 9. Responsive

Breakpoint único: **`max-width: 600px`**. En móvil:

- Header: `padding: 40px 24px 36px;` + ocultar `::before/::after` (glows)
- Grid: `grid-template-columns: 1fr;`
- Filter pills: `font-size: 10px; padding: 10px 14px;`
- Cards: `padding: 24px;`
- Milestones con imagen: apilar vertical (`flex-direction: column`)
- Ocultar scrollbar de nav pills

No añadir breakpoints intermedios salvo necesidad real.

---

## 10. Accesibilidad

### Obligatorio en toda página

1. **Skip link** antes del `<header>`:
   ```html
   <a href="#main" class="skip-link">Saltar al contenido</a>
   ```

2. **`:focus-visible`** con outline sólido:
   ```css
   :focus-visible { outline: 2px solid var(--ink); outline-offset: 2px; }
   .card:focus-visible { outline: 2px solid var(--card-accent, var(--ink)); outline-offset: 3px; }
   input:focus-visible, select:focus-visible, textarea:focus-visible { outline: none; }
   ```

3. **`lang="es"`** en `<html>`.

4. **Meta tags mínimos:** `description`, `og:title`, `og:description`, `og:image` (apuntando a `icon.svg`), `theme-color: #0f172a`.

5. **SVGs decorativos:** `aria-hidden="true"`.

6. **Botones sin texto visible:** `aria-label`.

7. **`prefers-reduced-motion`** (ver sección 8).

### Contraste

- Texto body: `#64748b` sobre `#ffffff` o `#e8edf4` → AA
- Links con color de zona anatómica: OK salvo columna (`#f59e0b` sobre blanco roza AA). Para texto largo en naranja, usar `--amber: #d97706` (más oscuro).

---

## 11. Navegación entre páginas

### Back-home (top-left de todas las páginas internas)

```html
<a class="back-home" href="{destino}.html" title="Volver">&larr; Volver</a>
```

Destino:
- Hub (`ptr.html`, `meniscos.html`, `lca.html`) → `index.html`
- Guía info/rehab → su hub (`ptr.html`, etc.)
- Guía sin hub (`infiltraciones.html`) → `index.html`

### Localhost detection

Todas las páginas incluyen al final del script:

```js
if (location.hostname === 'localhost' || location.hostname === '127.0.0.1') {
  document.querySelectorAll('a[href^="https://jmacot.github.io"]').forEach(function(a) {
    a.removeAttribute('href');
    a.style.opacity = '0.4';
    a.style.pointerEvents = 'none';
  });
}
```

Evita clicks a producción durante desarrollo local.

---

## 12. Añadir una nueva patología — checklist

Ver `CLAUDE.md` sección 5. En resumen:

- [ ] Crear `{patologia}.html` (hub) copiando `ptr.html`
- [ ] Crear `{patologia}-info.html` copiando `ptr-info.html`
- [ ] Crear `{patologia}-rehab.html` cuando haya rehabilitación
- [ ] Crear subcarpeta `img/{patologia}/`
- [ ] Añadir 1 card a `index.html` que enlace al hub
- [ ] Asignar filtro por zona anatómica (rodilla, cadera, hombro, columna)
- [ ] Si es zona nueva: añadir `--c-{zona}` y `--c-{zona}-light` en `:root` de index y del hub
- [ ] Verificar que las 8 secciones obligatorias están presentes
- [ ] Responsive manual (Chrome DevTools 375px)
- [ ] Comprobar navegación pills + scroll spy
- [ ] Verificar que no hay datos contradictorios con otras guías

---

## 13. Anti-patrones a evitar

1. **No añadir dark mode** — decisión consciente, ver sección 1.
2. **No usar sombra de capa única** (`0 2px 20px rgba(...)`). Siempre doble capa (STYLE-GUIDE ecosistema).
3. **No meter mesh gradient en hubs o guías** — solo landing.
4. **No usar backdrop-filter sin fallback de fondo opaco** — Firefox viejo.
5. **No usar emojis en contenido clínico** salvo `⚠️` en signos de alarma si aporta claridad.
6. **No usar "siempre" ni "nunca"** en datos médicos — "habitualmente", "en la mayoría".
7. **No modificar tiempos de recuperación** sin revisar todas las guías (info + rehab deben coincidir).
8. **No crear iconos nuevos por sección** — reutilizar los 8 estándar (sección 6.3).
9. **No publicar imágenes sin recortar** márgenes blancos.
10. **No romper la jerarquía de navegación:** `index → hub → info/rehab`. Las guías quirúrgicas nunca cuelgan directas del index.

---

## 14. Referencias cruzadas

- `COT/CLAUDE.md` — reglas de los sistemas A y B
- `COT/STYLE-GUIDE.md` — tokens CSS completos de ambos sistemas
- `pacientes/CLAUDE.md` — normas específicas del portal (estructura, datos médicos)
- `jmacot.github.io/index.html` — referencia viva del mesh gradient y el header compacto
