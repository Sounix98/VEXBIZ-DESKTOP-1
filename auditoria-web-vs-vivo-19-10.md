# Auditoría · VEXBIZ WEB (escritorio 1440) frente a ve.vexbiz.com en vivo (19/10)

Alcance: la propuesta de escritorio (`VEXBIZ WEB/`, base v1.9.13 + capa `web.css`/`web.js` del 05–06/10) comparada con el estado real de `ve.vexbiz.com` leído hoy directamente de su API (`marketplace-api/v1`, tenant `vepr`) y de la página renderizada a 1440 px. No se cambió nada del prototipo en la primera lectura: eso fue diagnóstico. Los puntos 1, 2 y 5 de la sección 4 ya se resolvieron (ver «Avance 19/10» al final).

## 1 · Qué cambió en el sitio en vivo desde la última lectura (30/09)

| Dato | 30/09 | Hoy (19/10) |
|---|---|---|
| Nichos | 16 | **20** — nuevos: Audio Profesional y Comercial, Equipos y Repuestos de Salud, Licorería, Maderas (se suman a Mascotas, Electronica, turismo, linea blanca, Construccion, ya nuevos el 30/09) |
| Productos | 2.073 | **2.223** |
| Tiendas | 25 | **32** |
| Técnicos | 57 | **64** |
| Cursos (Academia) | — | **8** |
| Ofertas relámpago | 6 productos, cierre 06/10 | **ya no existen** — la sección desapareció del home; solo queda una tarjeta genérica "Ofertas imperdibles · HOT -50%" dentro de "Explora por interés", y su filtro (`?deal=1`) no filtra nada: devuelve el catálogo completo (`matched_by: "browse"`, mismo total que sin filtro) |

Nichos con catálogo real hoy: Refrigeración 1.769, Automotriz 198, Ferretería 110, Farmacias 30, Restaurantes 39, Supermercados 19, Industrial 10, Motos 10, Telecomunicaciones 10, Mascotas 10, Electronica 11, Paneles Solares 8, linea blanca 4. El resto (Audio Profesional, Equipos de Salud, Licorería, GPS Trackers, turismo, Construccion, Maderas) sigue en 0.

## 2 · Estructura real del home en escritorio (1440px, verificado por API + captura)

Orden real de secciones: barra de confianza (4 íconos) → cabecera + buscador → nav de nichos → **hero de 3 banners** (Catálogo nacional / Técnicos certificados / Vende tus suministros — con mención expresa de "Escrow y liquidación garantizada") → grilla de 8 nichos con "Ver más" → Destacados de cada nicho (todo en "0 vendidos") → Servicios especializados (3 tarjetas: Técnicos, Auxilio vial, Seguros) → Tiendas oficiales y distribuidores (10) → banner Academia VEXBIZ → Marcas oficiales y homologadas (12 marcas — ninguna trae realmente `official: true` en la API pese al rótulo) → Explora por interés (4 nichos + Ofertas imperdibles) → **Por qué comprar en VexBiz** (6 viñetas) → Comunidad técnica (6 comunidades, todas en 0 actividad) → **Suscríbete a nuestro boletín** → pie de página (ver desglose exacto en «Avance 19/10», punto del footer).

Hallazgo técnico: las secciones `hero` y `sell_with_us` (banner de "Vende en VexBiz") vienen vacías en la API (`{"key":"hero"}`, sin `content`) — ese texto está escrito a mano en el frontend del sitio, no sale de datos. Para nuestro propio copy no hay una fuente de verdad que sincronizar; es contenido editorial libre.

## 3 · Qué ya tiene VEXBIZ WEB alineado con esto

- El hero de **3 banners** (Marketplace / Servicios / Para proveedores) en `home.js` ya sigue la misma lógica de 3 promociones del sitio real, con carrusel, puntos y pausa — coincide en forma, aunque el copy del tercero difiere (el nuestro dice "sin cuota de entrada, comisión sobre lo vendido"; el real dice "cobros protegidos con Escrow y liquidación garantizada").
- La franja de confianza de 4 íconos (`trust-strip`, usa `home.trust`) ya corresponde a la `trust_bar` real (Envíos rápidos · Devoluciones · Pago seguro · Soporte 24/7).
- "Proveedores certificados", "Explora por interés", "Marcas en VEXBIZ" y Comunidad técnica (dentro del recorrido) ya existen y son data-driven desde `api.home()` / `api.stores()` — en cuanto el snapshot tenga los datos nuevos, estos bloques los reflejan solos.
- El pie ya tiene sus 5 columnas reales (ver «Avance 19/10»).

## 4 · Lo que falta o diverge — de mayor a menor impacto

1. ~~**Snapshot de datos desactualizado (bloqueante para todo lo demás).**~~ **Resuelto 19/10** — ver «Avance 19/10».
2. ~~**Íconos de nicho faltantes.**~~ **Resuelto 19/10** — ver «Avance 19/10».
3. **Bloque "Por qué comprar en VexBiz" (6 viñetas) — no existe en `home.js`.** Es distinto de la franja de 4 íconos que sí tenemos: el sitio real lo muestra como sección aparte, más abajo, con Custodia de compra activa, Comercios auditados, Criterio técnico, Origen legítimo, Despacho seguro y Garantía sin trabas.
4. **Boletín de correo — no existe en el prototipo.** El sitio real cierra con un formulario "Suscríbete a nuestro boletín" antes del pie.
5. ~~**Pie de página con 3 columnas, no 5.**~~ **Resuelto 19/10** — ver «Avance 19/10».
6. **Copy del banner 3 ("Vende en VEXBIZ").** Diverge del mensaje real (Escrow / liquidación garantizada vs. "sin cuota de entrada"). Es contenido editorial libre (no viene de la API), así que es decisión de diseño, no un bug que corregir a ciegas. Pendiente de decidir con el usuario.
7. **Etiqueta "Marcas oficiales y homologadas".** Ninguna de las 12 marcas trae `official: true` en la API real; si en algún momento se quiere distinguir marca oficial de genérica en la tarjeta, hoy no hay dato que lo respalde.
8. **"Destacados" con 0 vendidos en todo.** Persiste desde auditorías anteriores (dato real, no de nuestro prototipo) — ya documentado, sin acción nueva de nuestro lado.

## 5 · Lo que NO hay que copiar

El sitio real no tiene el "recorrido infinito por nichos" (un bloque grande por nicho, con categorías y tiendas propias, cargando al bajar) que sí tiene nuestro prototipo — ahí la web real es una página de secciones fijas, más corta. Esa fue una decisión de diseño propia ya tomada (ver `home-recorrido-nichos-v1.9-30-09.md`) y pensada como mejora sobre el sitio real, no hay que revertirla para "parecerse más": se mantiene.

## Avance 19/10 — snapshot, íconos de nicho y pie de 5 columnas

**Snapshot regenerado.** Captura en vivo de `ve.vexbiz.com` vía `tools/snapshot.js` adaptado (sin el detalle por producto, ver nota) → `tools/build_catalog.py` → `data/catalog.json` nuevo: **2.223 productos, 32 tiendas, 20 nichos**, `fetched_at` 19/10/2026, coincide con los números de la sección 1. Se regeneró también `data/catalog.js` (modo doble clic / file://) y el bundle `assets/js/app.local.js`.

- **Trade-off a tener en cuenta:** esta captura es "ligera" — trajo los listados (precio, tienda, stock) de cada nicho, pero no el detalle por producto (`details`) ni las ofertas de otras tiendas (`offers`), para evitar más de 4.000 llamadas extra a la API. Efecto práctico: en esta versión del catálogo, la ficha de producto no va a mostrar descripción/atributos ni comparación de precio entre varias tiendas — cada producto solo trae su precio y tienda de origen. La captura del 30/09 sí traía eso, pero para un catálogo 6 veces más chico. Si se necesita ficha completa, hay que correr `tools/snapshot.js` sin recortar el paso de `details`/`offers` (más lento, muchas más llamadas).

**Íconos de nicho.** De los 20 nichos, 11 ya tenían arte propio en `assets/img/nichos/*.webp` (aut, far, fer, gps, ind, mot, ref, res, sol, sup, tlc). Los 9 restantes (Audio Profesional y Comercial, Equipos y Repuestos de Salud, Licorería, Mascotas, Electronica, turismo, linea blanca, Construccion, Maderas) no tienen ícono real todavía, así que se implementó un **monograma**: círculo con la(s) inicial(es) del nombre del nicho (misma función `initials()` que ya usan los logos de tienda sin logo propio) sobre el token `--vx-surface-2`, consistente con el resto del sistema. Se aplicó en los dos lugares donde `home.js` pinta el ícono de nicho: el carril de íconos (`nicon__bubble`) y la cabecera de cada bloque del recorrido (`nblock__ico`). Reemplazar un monograma por el ícono real a futuro es poner el `.webp` correspondiente en `assets/img/nichos/<id>.webp`: no hace falta tocar código, el fallback deja de activarse solo.

**Pie de 5 columnas.** Se leyó el DOM real del footer de `ve.vexbiz.com` (no solo los rótulos, también cada enlace y su destino) para no inventar contenido. Estructura real: columna de marca (logo, tagline, badges "Custodia Escrow" y "Tiendas Verificadas", más una fila aparte de "Redes Oficiales" con íconos sociales que no se replicó — ver pendiente abajo) + 4 columnas de enlaces — **Ayuda** (Cómo comprar, Envíos, Devoluciones y garantías, Contacto, Cómo se ve VexBiz), **Legal** (Términos y condiciones, Política de privacidad, Aviso legal), **Servicios** (Servicio técnico, Seguros, Auxilio vial, Academia), **Únete a VexBiz** (Vender en VexBiz, Trabajar como técnico, Franquicias, Quiénes somos, Nichos) — más una fila aparte (no una columna) de **Medios de pago** con las formas de pago reales (Transferencia bancaria, Pago móvil; se omitió el logo de pasarela "SPIDI" del sitio real por no tener el asset). `web.js` reemplazó el footer anterior (`Comprar` / `Tu cuenta` / `VEXBIZ`, 3 columnas inventadas) por este, con los mismos enlaces y destinos reales; como el prototipo no construye esas páginas (términos, envíos, franquicias...), cada enlace abre el sitio real en pestaña nueva, igual que ya hacía la columna "VEXBIZ" anterior — "Nichos" es la única que queda interna (`#/categorias`), porque esa vista sí existe en el prototipo. `web.css` pasó de una grilla de 4 a 5 columnas y sumó los estilos de las insignias y los chips de pago, todo con tokens `--vx-*` (cero hex a mano).

- **Pendiente, no bloqueante:** no se agregó la fila "Redes Oficiales" (Instagram/Facebook/TikTok/YouTube) del sitio real porque el sprite de íconos del proyecto no tiene esos glifos de marca todavía; si se quiere, hay que sumarlos al sprite primero.

Archivos tocados: `assets/js/views/home.js` (helper `nicheIco()`), `assets/js/web.js` (`FOOTER()` reescrito), `assets/css/app.css` (`.nicon__mono`), `assets/css/web.css` (`.df__in` a 5 columnas, `.df__badges`, `.df__pay`), `data/catalog.json`, `data/catalog.js`, `assets/js/app.local.js` (bundle regenerado). Verificado con capturas a 1440px (carril de nichos y pie) y a ancho móvil (bloque del recorrido) antes de entregar.

## 6 · Próximo paso

Con el snapshot, los íconos y el pie resueltos, lo que queda del punto 4 es: el bloque "Por qué comprar en VexBiz" (6 viñetas), el boletín de correo, y la decisión pendiente sobre el copy del banner 3 (Escrow vs. mensaje actual).
