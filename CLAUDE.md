# Plantilla «Clínica dental» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **limpio**
(concepto «sala con luz», ver `DISEÑO.md`). Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y `src/styles/global.css` saca los derivados con `color-mix` (`--cielo`, `--cielo-2`, `--menta`, `--noche`, `--tinta`, `--linea`). Tailwind los expone como `bg-primario`, `text-acento`…
- **Tipografías y aspecto general**: `src/styles/global.css` (bandas `.banda` + `.tono-*`, antetítulo con punto y línea, `.sonrisa` bajo la última palabra de los títulos, botones `.btn`/`.btn-sec`/`.btn--menta`, `.icono-caja`, `.etiqueta`, cabecera y pie). Fuentes del sistema redondeadas: no añadas fuentes externas.
- **Bandas**: cada sección usa `src/components/ui/Seccion.astro` con un `tono` (`claro`, `cielo`, `menta`, `primario`, `acento`, `noche`). Las bandas son planas y van de borde a borde; no metas una sección en una caja estrecha.
- **Imágenes**: en `public/`. Las de relleno están en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos nuevas del cliente van en `public/fotos/`. Personas: `/placeholders/persona.svg` mientras no haya foto.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = diente blanco en cuadrado azul y el nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`.
- `hero` → `src/components/secciones/hero.astro` (partida 50/50, foto a sangre a la derecha, garantías y ficha `destacado`)
- `tratamientos` → `tratamientos.astro` (agrupados por `categoria`)
- `financiacion` → `financiacion.astro` (cifra, pasos y ventajas)
- `equipo` → `equipo.astro`
- `tecnologia` → `tecnologia.astro` (50/50 con foto a sangre + franja de galería)
- `primera-visita` → `primera-visita.astro` (banda menta con llamada a la acción)
- `opiniones` → `opiniones.astro`
- `preguntas` → `preguntas.astro`
- `cita` → `cita.astro` (formulario con tratamiento y franja horaria, `src/components/ui/FormularioCita.astro`)
- `contacto` → `contacto.astro` (horario grande, datos y foto; si `cita` no está activa, también el formulario de contacto)
- `texto` → `texto.astro` (genérico para apartados nuevos con `tipo: texto`)

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas, como texto.
4. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`, con bandas (`<section class="banda tono-cielo">…`); enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
5. **Sección nueva**: crea `src/components/secciones/<id>.astro` (copia la estructura de una existente: `seccion(id)`, `Seccion` con su `tono`, `Titular`) y añade `secciones.<id>` en `site.yaml`. `src/pages/index.astro` la recoge sola.
6. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
7. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto en móvil (las fotos y los fondos sí tocan el borde), sin scroll horizontal a 375 px, botones de 44 px de alto como mínimo. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el `titulo`/`nombre` de la ficha); las decorativas, `alt=""`.
8. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioCita.astro` y `FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `hero.items` {titulo, icono}: garantías en fila bajo los botones. `hero.destacado` {titulo, texto}: ficha blanca sobre la foto («Primera visita gratis»). `hero.cta_secundario`: segundo botón.
- `tratamientos.tratamientos` {nombre, texto, precio, duracion, categoria, icono}: precio como cadena («desde 45 €», «Gratis», «Consultar»); se agrupan por `categoria` en el orden en que aparecen.
- `financiacion.destacado` {titulo, texto}: cifra grande («0 %» · «de interés…»). `financiacion.items` {titulo, texto, icono, categoria}: `categoria: Paso` = pasos numerados; `Ventaja` (o vacía) = ventajas con icono. `financiacion.cta`.
- `tecnologia.items` {titulo, texto, icono}, `tecnologia.imagen`, `tecnologia.galeria` (franja de fotos de borde a borde, hasta 6).
- `primera-visita.items` {titulo}: lo que incluye. `cta`, `cta_secundario`, `nota`, `imagen`.
- `cita.opciones`: tratamientos del desplegable, separados por «;». `cita.franjas`: franjas horarias, separadas por «;». `cita.items` {titulo}: pasos. `cita.cta.texto`: botón de WhatsApp (destino `cta.url` o, vacío, el WhatsApp de contacto). `cita.imagen`.
- `contacto.horario` {dia, horas}: horario en grande; `contacto.imagen` (fachada; el botón «Cómo llegar» abre el mapa).

Iconos disponibles (`icono`): los de `src/components/ui/Icono.astro`, entre ellos `diente`, `implante`, `brackets`, `chispa`, `cepillo`, `rayosx`, `escaner`, `sillon`, `microscopio`, `nino`, `escudo`, `porcentaje`, `tarjeta`, `euro`, `calendario`, `reloj`, `usuarios`, `check`.

Fotos de partida en `public/fotos/` (las genera el paso de fotos a partir de `fotos.json`, sin derechos de terceros); los SVG de `public/placeholders/` siguen de respaldo.
