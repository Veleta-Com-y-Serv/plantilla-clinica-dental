# Plantilla «Clínica dental» · NoExpertise

Web de una sola página para clínicas dentales, dentistas, ortodoncia, implantes y odontopediatría. Estilo **limpio**,
a ancho completo y responsive (concepto «sala con luz», ver `DISEÑO.md`). Astro 5 + Tailwind 4, derivada de
AstroWind (MIT, `LICENSE-ASTROWIND.md`). Todo el contenido sale de `site.yaml`.

Ejemplo: *Clínica Dental Aguamarina*, un negocio ficticio del centro de Almería.

## Secciones
| id | Qué es | Campos propios |
|---|---|---|
| `hero` | Portada partida 50/50 con foto a sangre | `items` {titulo, icono} (garantías), `destacado` {titulo, texto}, `cta_secundario` |
| `tratamientos` | Tratamientos por categoría | `tratamientos` {nombre, texto, precio, duracion, categoria, icono} |
| `financiacion` | Pago a plazos | `destacado` {titulo, texto}, `items` {titulo, texto, icono, categoria «Paso» o «Ventaja»}, `cta` |
| `equipo` | Equipo | `personas` {nombre, cargo, foto, texto} |
| `tecnologia` | Equipamiento | `imagen`, `items` {titulo, texto, icono}, `galeria` |
| `primera-visita` | Llamada a la acción | `imagen`, `items` {titulo}, `cta`, `cta_secundario`, `nota` |
| `opiniones` | Opiniones | `testimonios` {texto, autor} |
| `preguntas` | Preguntas frecuentes | `preguntas` {pregunta, respuesta} |
| `cita` | Formulario de cita | `imagen`, `opciones` («;»), `franjas` («;»), `items` {titulo}, `cta` (WhatsApp) |
| `contacto` | Horario, datos y fachada | `horario` {dia, horas}, `imagen` |
| `texto` | Apartado genérico (`tipo: texto`) | `items`, `imagen`, `cta` |

Precios siempre como cadena («desde 45 €», «Gratis», «Consultar»); sin precio no se pinta. Todo lo que esté vacío
desaparece sin romper el diseño.

## Construir
```
npm ci && npm run build
npx astro preview
```

Fotos: `fotos.json` (las genera el paso de fotos); respaldo en `public/placeholders/`.

## Páginas propias
- Cada elemento de `secciones.tratamientos.tratamientos` con `detalle` tiene su página en `/tratamientos/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
