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
index.html          ← Landing page: 1 card por patología + "Quién soy"
ptr.html            ← Hub PTR: 2 subcards (info + rehab)
ptr-info.html       ← Guía PTR: información y expectativas
meniscos.html       ← Hub Meniscos: 2 subcards (info + rehab)
meniscos-info.html  ← Guía Meniscos: información y expectativas
meniscos-rehab.html ← Guía Meniscos: rehabilitación postoperatoria
infiltraciones.html ← Guía Infiltraciones: comparativa corticoides/HA/PRP (enlace directo, sin hub)
img/                ← Imágenes de las guías
```

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
6. **Imágenes:** Todas las guías deben tener al menos 1-2 imágenes ilustrativas. Formato `.jpg` o `.png`, guardadas en `img/` con nombre descriptivo (`{patologia}-{descripcion}.jpg`)
8. **Imágenes en milestone cards (Recuperación):** Cuando una milestone card incluye una imagen ilustrativa, usar layout `milestone-content` (flex horizontal) con la imagen en un `milestone-aside` a la derecha del texto (width: 300px, max-width: 300px). En móvil (`max-width: 600px`) se apilan verticalmente. **Nunca** apilar la imagen debajo del texto en desktop — queda demasiado espacio en blanco y alarga innecesariamente la card
7. **Durabilidad/pronóstico:** Siempre usar un tono realista pero positivo. No dar por hecho resultados negativos. Ejemplo: "La mayoría duran más de 20 años" en vez de "Duran 15-20 años"

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

Al crear una nueva guía (ej. `lca-info.html`):

- [ ] Crear archivo `{patologia}-info.html` copiando estructura de `ptr-info.html`
- [ ] Adaptar contenido de las 8 secciones obligatorias
- [ ] Verificar coherencia con la guía de rehabilitación correspondiente
- [ ] Añadir imágenes en `img/` (mínimo 1)
- [ ] Añadir 2 cards en `index.html` (Información + Rehabilitación)
- [ ] Verificar filtro por zona anatómica
- [ ] Verificar dark mode y responsive
- [ ] Verificar navegación pills y scroll spy
- [ ] Comprobar que no hay datos contradictorios con otras guías
