# Clínica dental — brief de diseño

Plantilla de la tercera tanda «ancho completo» (02/11/2026), creada a partir de `veterinaria` (solo su estructura
técnica: `index.astro`, `src/lib/seo.ts`, endpoints, `src/data/site.ts`, `Imagen.astro`, formularios `mailto` y
`Base.astro`). Todo lo visual es nuevo.

## Concepto: «sala con luz»
Una clínica dental limpia y luminosa, sin frialdad de hospital. Bandas planas a todo el ancho que alternan blanco,
cielo muy pálido, azul cielo pleno, menta plena y azul noche; mucho aire; esquinas de 1 rem en todo (botones,
fotos que no tocan el borde, fichas, campos). El sello de la plantilla es la **sonrisa**: un arco menta bajo la
última palabra de cada título (`.sonrisa`). Antetítulos en mayúsculas con interletrado, un punto menta con halo y
una línea menta.

## Paleta (de las cuatro variables de `site.yaml`)
- `--c-primario` azul cielo `#1a74c4` (bandas plenas, botones, precios, iconos).
- `--c-acento` menta `#5fd3b5` (sonrisa, banda de primera visita, botones sobre azul).
- `--c-fondo` blanco y `--c-texto` azul tinta `#0f2a3d`.
- Derivados con `color-mix`: `--cielo` y `--cielo-2` (fondos pálidos), `--menta` (fondo pálido), `--noche`
  (azul noche del apartado de tecnología y del pie), `--tinta` (texto sobre menta), `--linea`.

## Tipografía
Pila de sistema redondeada: `ui-rounded`, «SF Pro Rounded», «Nunito», «Arial Rounded MT Bold», Segoe UI… a 800 en
títulos (hero 2.6-5.75 rem, secciones 2.1-4 rem), texto a 17 px con interlineado 1.7. Sin fuentes externas.

## Secciones (orden del ejemplo y banda)
1. `hero` — partida 50/50 a pantalla casi completa: texto sobre cielo pálido a la izquierda (título, texto, dos
   botones, garantías `items` en fila) y foto a sangre a la derecha con la ficha blanca `destacado`. En móvil, la
   foto debajo, a sangre.
2. `tratamientos` (blanco) — lista propia `tratamientos` {nombre, texto, precio, duracion, categoria, icono}; un
   bloque por categoría: nombre grande fijo a la izquierda y rejilla de celdas con líneas finas (3 columnas).
3. `financiacion` (azul cielo pleno) — `destacado` en cifra enorme, pasos (`items` con `categoria: Paso`) en línea
   vertical y ventajas (`categoria: Ventaja`) en 4 columnas.
4. `equipo` (blanco) — `personas` en 4 columnas, retrato 3:4; en móvil, carrusel lateral.
5. `tecnologia` (azul noche) — foto a sangre a la izquierda, equipamiento `items` en 2 columnas y franja de fotos
   `galeria` de borde a borde.
6. `primera-visita` (menta plena) — llamada a la acción con lista de lo que incluye, dos botones, `nota` y foto a
   sangre a la derecha.
7. `opiniones` (blanco) — la primera opinión como cita enorme y el resto en 3 columnas con líneas.
8. `preguntas` (cielo pálido) — titular fijo con teléfono y WhatsApp a la izquierda y acordeón a la derecha.
9. `cita` (menta pálida) — foto a sangre a la izquierda y formulario con tratamiento (`opciones`) y franja horaria
   (`franjas`) en panel blanco.
10. `contacto` (blanco) — panel azul cielo a sangre con el horario en grande, datos con icono y foto de la fachada.
- `texto` — genérico (cielo pálido, con foto a sangre opcional).

Cabecera fija siempre sólida (blanca translúcida) con diente en cuadrado azul, menú, teléfono y botón; pie azul noche
con cuatro columnas y la ficha menta «Pedir cita».

## Lo que la distingue
De `veterinaria`: nada de bandas con esquinas que se solapan ni chapas redondas ni coral; hero partido en vez de foto
con velo. De las demás: la sonrisa bajo el título, la rejilla de tratamientos por categoría con líneas finas y la
paleta blanco + cielo + menta.

## Páginas propias (fichas)
Con la misma piel que la portada: cabecera y pie de la plantilla, migas (Inicio › Sección › Elemento), hero con la foto del
elemento (sin foto, su icono), `detalle` en párrafos, tabla de datos, caja de contacto, galería (`imagenes`) y otros elementos
de la misma lista.
