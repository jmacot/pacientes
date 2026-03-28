# 🩺 Informacion para Pacientes

Portal de informacion para pacientes del Dr. Martin Antunez. Guias de rehabilitacion, ejercicios y cuidados postoperatorios para cirugia de rodilla.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![Guias](https://img.shields.io/badge/guias-4-1a3a5c)
![Sin dependencias](https://img.shields.io/badge/dependencias-ninguna-grey)

---

## Acceso

> Acceso publico — dirigido a pacientes, no requiere autenticacion.

[Abrir el portal](https://jmacot.github.io/pacientes/)

---

## Contenido

### Protesis Total de Rodilla (PTR)
- **Informacion y expectativas**: estancia hospitalaria, recuperacion mes a mes, heparina, signos de alarma, FAQ
- **Rehabilitacion postoperatoria**: fases, ejercicios, hitos funcionales

### Lesiones Meniscales
- **Informacion y expectativas**: tipos de lesion, tratamiento, proceso hospitalario, recuperacion
- **Rehabilitacion postoperatoria**: protocolo por fases, ejercicios, retorno a la actividad

---

## Funcionalidades

- **Navegacion por patologia**: hub intermedio con subcards de informacion y rehabilitacion
- **Acordeones nativos** (`<details>/<summary>`) para organizar el contenido
- **Navegacion sticky con pills** y scroll spy automatico
- **Imagenes ilustrativas** para facilitar la comprension
- **Timeline de recuperacion** con milestones por mes
- **Tabla expectativas vs realidad** para desmontar mitos frecuentes
- **Signos de alarma** destacados en callout rojo
- **FAQ** con mini-acordeones
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
├── index.html            ← landing page con cards por patologia
├── ptr.html              ← hub PTR (info + rehab)
├── ptr-info.html         ← guia PTR: informacion y expectativas
├── meniscos.html         ← hub Meniscos (info + rehab)
├── meniscos-info.html    ← guia Meniscos: informacion
├── meniscos-rehab.html   ← guia Meniscos: rehabilitacion
├── img/                  ← imagenes de las guias
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
