# Normas del Portal de Pacientes

> Reglas para crear y mantener contenido en `jmacot.github.io/pacientes/`

---

## 1. Identidad del portal

- **Autor:** Dr. Javier Martín Antúnez — Cirujano Ortopédico, Especialista en Rodilla
- **Hospital:** Vithas Sevilla
- **Público objetivo:** Pacientes (no profesionales médicos). Lenguaje claro, cercano, sin tecnicismos innecesarios
- **Propósito:** Elemento diferenciador — ofrecer información personalizada que otros cirujanos no proporcionan
- **Sistema de diseño:** Sistema A (Editorial) del CLAUDE.md principal de COT

---

## 2. Estructura del portal

```
index.html           ← Landing page: 1 card por patología + "Quién soy"

ptr.html             ← Hub PTR
ptr-info.html        ← Guía PTR: información y expectativas
                       (pendiente: ptr-rehab.html)

meniscos.html        ← Hub Meniscos
meniscos-info.html   ← Guía Meniscos: información y expectativas
meniscos-rehab.html  ← Guía Meniscos: rehabilitación postoperatoria

lca.html             ← Hub LCA
lca-info.html        ← Guía LCA: información y expectativas
                       (pendiente: lca-rehab.html)

infiltraciones.html  ← Guía tratamiento: corticoides / HA / PRP (enlace directo, sin hub)
animacion-prp.html   ← Animación interactiva SVG embebida como iframe/modal desde infiltraciones.html

icon.svg             ← Favicon + apple-touch-icon + og:image (compartido por todas las páginas)
CLAUDE.md, README.md, .gitignore

img/                 ← Imágenes organizadas por patología (ver abajo)
qr/                  ← Códigos QR (pacientes, ptr) en PNG + SVG
.claude/             ← Configuración local de Claude Code (launch.json, settings)
```

### Organización de `img/`

Las imágenes están separadas por patología para que sea fácil localizarlas y asociarlas con sus guías:

```
img/
├── logos/          ← Logos institucionales (vithas, osten…)
├── compartidas/    ← Imágenes multi-guía (heparina, rodillera, artroscopia, bicicleta, elevación pierna recta)
├── ptr/            ← Específicas de PTR (antes/después, implante, unicompartimental)
├── meniscos/       ← Específicas de meniscos (lesiones, raíz, vascularización)
├── lca/            ← Específicas de LCA (mecanismo lesión, plastia, injertos)
├── infiltraciones/ ← Específicas de infiltraciones (corticoide, hialurónico)
└── _archivo/       ← Imágenes no utilizadas (base para futuros retoques o eliminación)
```

**Regla:** al añadir una imagen nueva, colócala en la subcarpeta de la patología a la que pertenece. Si la imagen puede reutilizarse en más de una guía (p. ej. un ejercicio de rehabilitación, una inyección), va en `compartidas/`. Actualiza el `src` de los HTML con la ruta completa: `img/{subcarpeta}/{nombre}.png`.

### Arquitectura de navegación — REGLA CRÍTICA

**Patologías quirúrgicas** siguen una estructura de **3 niveles**:

1. **`index.html`** — 1 sola card por patología (ej. "Lesiones Meniscales") que enlaza al hub
2. **`{patologia}.html`** (hub) — Página intermedia con subcards: Información + Rehabilitación. Sigue la estructura exacta de `ptr.html`
3. **`{patologia}-info.html`** y **`{patologia}-rehab.html`** — Páginas de contenido

**Nunca** poner cards de info y rehab directamente en index.html. Siempre usar el hub intermedio.

**Guías de tratamiento** (ej. infiltraciones) usan **enlace directo** desde index.html → `{tratamiento}.html`. No necesitan hub intermedio porque son una sola página sin componente de rehabilitación.

### Landing page (`index.html`)

- Título: "Información para Pacientes / Dr Martín Antúnez"
- **1 card por patología** que enlaza al hub (`{patologia}.html`), con detalle "2 guías disponibles"
- Sección "Sobre el cirujano" con perfil, formación y enlaces
- Filtros por zona anatómica (rodilla, etc.)

### Páginas hub (`{patologia}.html`)

- Estructura idéntica a `ptr.html`: header con título de patología + grid de 2 cards
- Card 1: Información y Expectativas → `{patologia}-info.html`
- Card 2: Rehabilitación Postoperatoria → `{patologia}-rehab.html`
- Back link: `index.html`
- Localhost detection JS

### Páginas de información (`{patologia}-info.html`)

- Una página por patología siguiendo el patrón de `ptr-info.html`
- Acordeones `<details>/<summary>` nativos
- Navegación sticky por pills con scroll spy
- Primera sección abierta por defecto, resto cerradas

---

## 3. Coherencia entre patologías — REGLA CRÍTICA

**Todas las guías de información deben seguir la misma estructura de secciones.** Cuando se cree una nueva guía (ej. artroscopia, LCA, osteotomías), debe contener las mismas secciones que PTR, adaptadas al contenido específico:

### Secciones obligatorias (en este orden):

| # | Sección | Contenido |
|---|---------|-----------|
| 1 | **Introducción** | Qué es la cirugía, indicaciones, tipos/variantes, actividades recomendadas vs evitar (si aplica), complicaciones posibles |
| 2 | **Estancia hospitalaria** | Timeline: día cirugía → días postoperatorios → alta. Tratamiento al alta, calendario de revisiones |
| 3 | **Administración de heparina** | Pasos de inyección subcutánea, duración (30 días salvo indicación diferente), señales de alerta |
| 4 | **Recuperación mes a mes** | 4 milestones temporales con hitos de dolor, movilidad, actividad. Adaptar tiempos a la patología |
| 5 | **Expectativas vs. Realidad** | Tabla comparativa con mitos frecuentes del paciente vs realidad clínica |
| 6 | **Cosas que debes saber** | Lista numerada con mensajes clave (adaptar número según patología) |
| 7 | **Signos de alarma** | Callout rojo con señales que requieren urgencias |
| 8 | **Preguntas frecuentes** | FAQ en mini-acordeones, mínimo 5 preguntas |

### Secciones opcionales (añadir si aplica):

- **Preparación preoperatoria** — qué hacer antes de la cirugía
- **Consejos para el domicilio** — adaptaciones en casa, ayudas técnicas
- **Ejercicios básicos** — con imágenes o vídeos

### Reglas de coherencia:

1. **Misma estructura visual:** Todas las guías usan los mismos componentes CSS (acordeones, timelines, callouts, milestone cards, tablas comparativas, FAQ)
2. **Mismos iconos por sección:** Introducción = 🧩, Hospital = 🏥, Heparina = 💉, Recuperación = 📈, Expectativas = 📊, Claves = 💬, Alarma = ⚠️, FAQ = ❓
3. **Misma navegación:** Pills sticky con los mismos nombres de sección
4. **Datos médicos concordantes:** Si una guía de información menciona un plazo (ej. "conducir a las 6 semanas"), la guía de rehabilitación correspondiente debe decir lo mismo. **Nunca publicar datos contradictorios entre la página de información y la de rehabilitación**
5. **Tono consistente:** Tutear al paciente, frases cortas, bullet points, negrita para lo importante
6. **Imágenes:** Todas las guías deben tener al menos 1-2 imágenes ilustrativas. Formato `.jpg` o `.png`, guardadas en la subcarpeta correspondiente de `img/` (ver sección 2). Nombre descriptivo sin prefijo de patología (la subcarpeta ya identifica la patología): `img/ptr/antes-despues.jpg` en vez de `img/ptr-antes-despues.jpg`. Usar clases `.info-img`, `.info-img.medium` (max 420px) o `.info-img.small` (max 280px) — ambas usan `min(Xpx, 100%)` para no desbordar en móvil.

   **Recorte de márgenes blancos** — antes de añadir una imagen, eliminar los márgenes en blanco con Pillow:

   ```python
   from PIL import Image, ImageChops
   ruta = 'img/{subcarpeta}/nombre.png'
   img = Image.open(ruta)
   bg = Image.new('RGB', img.size, (255, 255, 255))
   bbox = ImageChops.difference(img.convert('RGB'), bg).getbbox()
   if bbox:
       pad = 40
       bbox = (max(0,bbox[0]-pad), max(0,bbox[1]-pad), min(img.width,bbox[2]+pad), min(img.height,bbox[3]+pad))
       img.crop(bbox).save(ruta, optimize=True)
   ```

   Si el fondo no es blanco puro (el bbox devuelve el tamaño completo), la imagen ya está bien recortada — no hace falta procesarla.
7. **Imágenes en milestone cards (Recuperación):** Cuando una milestone card incluye una imagen ilustrativa, usar layout `milestone-content` (flex horizontal) con la imagen en un `milestone-aside` a la derecha del texto (width: 300px, max-width: 300px). En móvil (`max-width: 600px`) se apilan verticalmente. **Nunca** apilar la imagen debajo del texto en desktop — queda demasiado espacio en blanco y alarga innecesariamente la card
8. **Durabilidad/pronóstico:** Siempre usar un tono realista pero positivo. No dar por hecho resultados negativos. Ejemplo: "La mayoría duran más de 20 años" en vez de "Duran 15-20 años"

---

## 4. Datos médicos — reglas de redacción

- **No contradecir** datos entre la guía de información y la de rehabilitación postoperatoria
- **Especificar contexto** cuando un dato depende del caso (ej. conducir: diferenciar rodilla izquierda vs derecha)
- **Tono positivo realista:** Los pacientes leen esto antes o después de operarse. No minimizar riesgos pero no generar ansiedad innecesaria
- **No usar "siempre" ni "nunca"** en contextos médicos — usar "habitualmente", "en la mayoría de los casos", "puede variar"
- **Complicaciones:** Mencionar las principales pero en contexto ("si bien la tasa de éxito es alta...")
- **Recambio protésico:** No dar por hecho. Mensaje: la mayoría duran décadas, el recambio no es lo habitual

---

## 5. Checklist para nueva patología

Al crear una nueva guía (ej. `osteotomias.html` + `osteotomias-info.html` + `osteotomias-rehab.html`):

- [ ] Crear el **hub** `{patologia}.html` copiando estructura de `ptr.html` (header + 2 subcards)
- [ ] Crear `{patologia}-info.html` copiando estructura de `ptr-info.html`
- [ ] Crear `{patologia}-rehab.html` cuando haya material de rehabilitación
- [ ] Adaptar contenido de las 8 secciones obligatorias de la guía de información
- [ ] Crear subcarpeta `img/{patologia}/` y añadir imágenes propias (mínimo 1)
- [ ] Reutilizar imágenes de `img/compartidas/` si aplica (heparina, rodillera, artroscopia, bicicleta…)
- [ ] Añadir **1 card** en `index.html` que enlace al hub (no cards directas info/rehab)
- [ ] Asignar filtro por zona anatómica correspondiente
- [ ] Verificar responsive (móvil/tablet/desktop)
- [ ] Verificar navegación pills sticky + scroll spy
- [ ] Comprobar que no hay datos contradictorios con otras guías

> **Nota:** el portal **no tiene dark mode** ni sky toggle (decisión del autor para mantener una única identidad visual clara). No añadirlo.
