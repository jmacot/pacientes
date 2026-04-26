# 🩺 Informacion para Pacientes

Portal de informacion para pacientes del Dr. Martin Antunez. Guias de rehabilitacion, ejercicios y cuidados postoperatorios para cirugia de rodilla.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![Guias](https://img.shields.io/badge/guias-7-1a3a5c)
![Sin dependencias](https://img.shields.io/badge/dependencias-ninguna-grey)

---

## Acceso

> Acceso publico — dirigido a pacientes, no requiere autenticacion.

[Abrir el portal](https://jmacot.github.io/pacientes/)

---

## Contenido

### Lesiones Meniscales (card hero del landing)
- **Informacion y expectativas**: tipos de lesion, tratamiento, proceso hospitalario, recuperacion
- **Rehabilitacion postoperatoria**: protocolo por fases, ejercicios, retorno a la actividad
- **Slideshow de consulta**: secuencias de sutura meniscal en fila

### Reconstruccion del LCA
- **Informacion y expectativas** del proceso quirurgico y recuperacion

### Protesis Total de Rodilla (PTR)
- **Informacion y expectativas**: estancia hospitalaria, recuperacion mes a mes, heparina, signos de alarma, FAQ
- Imagen de implante de alta calidad reutilizada de `rehabilitacion-cot`

### Infiltraciones
- **Guia ampliada de infiltraciones**: indicaciones, productos (corticoide, AH, PRP), tecnica
- **Animacion explicativa de PRP** (`animacion-prp.html`)
- **Boton Descargar PDF** con estilos `@media print`

---

## Funcionalidades

- **Landing con bento grid**, estética unificada con `jmacot.github.io`
- **Navegacion por patologia**: hub intermedio con subcards de informacion y rehabilitacion
- **Apartado consulta/** con slideshows visuales para enseñar al paciente en consulta
- **Acordeones nativos** (`<details>/<summary>`) para organizar el contenido
- **Navegacion sticky con pills** y scroll spy automatico
- **Imagenes ilustrativas optimizadas** (compresion masiva: 83 MB liberados respecto al primer release)
- **Timeline de recuperacion** con milestones por mes, sin cortes entre páginas en PDF
- **Tabla expectativas vs realidad** para desmontar mitos frecuentes
- **Signos de alarma** destacados en callout rojo
- **FAQ** con mini-acordeones
- **Descarga PDF** con `window.print()` y CSS print canónico (sin header del navegador, sin saltos de línea problemáticos)
- **Modo oscuro** con deteccion automatica
- **Responsive** para consulta desde el movil del paciente

---

## Como usar

1. Selecciona tu **patologia** en la pagina principal
2. Elige entre **Informacion** (que esperar) o **Rehabilitacion** (que hacer)
3. Navega por las **secciones** usando las pills superiores
4. Despliega los **acordeones** para ver el contenido de cada tema

---

## Estructura del proyecto

```
pacientes/
├── index.html            ← landing page con bento grid (Meniscos hero, PTR/LCA medium, Infiltraciones)
├── meniscos.html         ← hub Meniscos (info + rehab)
├── meniscos-info.html    ← guia Meniscos: informacion
├── meniscos-rehab.html   ← guia Meniscos: rehabilitacion
├── lca.html              ← hub LCA
├── lca-info.html         ← guia LCA: informacion
├── ptr.html              ← hub PTR (info)
├── ptr-info.html         ← guia PTR: informacion y expectativas
├── infiltraciones.html   ← guia ampliada de infiltraciones (corticoide, AH, PRP)
├── animacion-prp.html    ← animacion didactica del PRP
├── consulta/             ← slideshows visuales para mostrar al paciente en consulta
├── img/                  ← imagenes optimizadas, organizadas por patologia
├── qr/                   ← QR para acceso rapido desde consulta
├── .gitignore
└── README.md             ← este archivo
```

---

## Tecnologia

- **HTML5 + CSS3 + JavaScript vanilla**
- Tipografias: [DM Sans](https://fonts.google.com/specimen/DM+Sans), [DM Serif Display](https://fonts.google.com/specimen/DM+Serif+Display) y [DM Mono](https://fonts.google.com/specimen/DM+Mono) (Google Fonts)
- Sistema de diseno A (Editorial) del ecosistema COT
- Sin frameworks, sin build tools, sin backend

---

## Licencia

MIT
