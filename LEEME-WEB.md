# VEXBIZ WEB · Aproximación de escritorio (1440 px)

Prototipo aparte de la app móvil: misma base (v1.9.13, mismos tokens, datos y pantallas) con una capa de escritorio en `assets/css/web.css` y `assets/js/web.js`. La app móvil (carpeta VEXBIZ APP) no cambia.

## Cómo verlo
Doble clic en `index.html` y abre la ventana a 1024 px o más (pensado para 1440). Por debajo de 1024 px se ve igual que la app móvil.

## Qué cambia en escritorio
- Sin marco de teléfono ni tab bar. Cabecera superior: logo, "Enviar a", buscador ancho, Pedidos, Favoritos, Entrar/Cuenta y Carrito con contador. Debajo, barra con los 11 nichos, "Todas las categorías" y "Tiendas".
- Contenido centrado en 1280 px; pie de página con enlaces en todas las vistas.
- Buscador (06/10): una sola pieza de 48 px al estilo Mercado Libre/Amazon. A la izquierda el alcance (Todo o un nicho), campo amplio, borrar y lupa ámbar pegada a la derecha. Al enfocar muestra búsquedas recientes, lo más buscado y nichos; al escribir, «Buscar …» con el total y hasta 6 productos con foto y precio (flechas, Enter y Esc funcionan). Con un nicho elegido busca solo dentro de él.
- Portada (06/10): carrusel a todo el ancho debajo del buscador con 5 imágenes (Marketplace, Refrigeración, Automotriz, Técnicos, Vende en VEXBIZ) compuestas con fotos reales del catálogo y los íconos 3D de nicho. Cambia cada 6 s con fundido y entrada escalonada; la barra ámbar muestra el tiempo. Se pausa al pasar el mouse, al enfocar o con el botón de pausa; flechas a los lados. Con movimiento reducido no avanza sola.
- Inicio: Academia y nichos centrados, Academia y nichos centrados, Ofertas relámpago en grilla de 6, proveedores en carrusel de una fila con flechas, Explora por interés en una fila de 6. Luego el recorrido: por cada nicho con productos, una fila de 6 productos (sin repetir los de arriba) con «Explorar <nicho>», y entre filas un banner de llamado a la acción (Técnicos, Auxilio vial, Academia, Seguros). Cierra con Comunidad técnica, Marcas, confianza y pie. El detalle de cada nicho (categorías, tiendas) vive en su página.
- Nicho: filtros de categoría en columna izquierda, orden arriba y productos en 4 columnas.
- Ficha: galería fija a la izquierda, compra a la derecha; relacionados en grilla de 6.
- Buscar: el buscador de la cabecera reemplaza al de la pantalla; resultados en tarjetas de 5 columnas.
- Carrito y Entrega y pago: contenido a la izquierda, resumen y botón a la derecha (fijo al bajar).
- Cuenta, Pedidos: columna de lectura de 880 px. Entrar y Crear cuenta: tarjeta centrada de 520 px.
- La hoja de "Enviar a" se abre como diálogo centrado.

## Capturas
`capturas-1440/`: las 15 vistas en tema claro y oscuro (página completa), `00-resumen-*.jpg` con todas juntas, `16-portada-1..5-*.jpg` (cada imagen del carrusel) y `17-buscador-*.jpg` (sugerencias).
