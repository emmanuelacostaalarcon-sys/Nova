# Handoff: NOVA General Electric — tienda web y app móvil

## Overview

NOVA General Electric es una tienda de materiales eléctricos (Chile, CLP). El paquete cubre dos superficies:

- **Web de escritorio/tablet/móvil**: home, catálogo por categoría con filtros, buscador, carrito con checkout, cuenta con historial de pedidos, y contacto.
- **App móvil**: home, catálogo con filtros, buscador (escáner de código y calce de lista de materiales), carrito con checkout y cuenta.

Público: instaladores eléctricos que recompran los mismos materiales, y público general de ferretería.

## About the Design Files

Los archivos de este paquete son **referencias de diseño construidas en HTML**: prototipos que muestran el aspecto y el comportamiento buscado, no código de producción para copiar. La tarea es **recrear estos diseños en el entorno del codebase destino** (React, Vue, SwiftUI, nativo, etc.) usando sus patrones y librerías establecidas. Si aún no existe un entorno, elige el framework adecuado e impleméntalos ahí.

Los prototipos usan estilos en línea y una capa de plantillas propia del entorno de diseño. Nada de eso debe trasladarse: extrae los valores (colores, tipografía, medidas, copy) y reconstruye con los componentes del proyecto.

## Fidelity

**Alta fidelidad.** Colores, tipografía, espaciado, estados y copy son definitivos. Recréalos con precisión.

Excepción: las imágenes de producto son ilustraciones SVG planas de relleno, no fotografía final. Ver "Assets".

## Design Tokens

### Color

| Rol | Hex | Uso |
| --- | --- | --- |
| Azul marino primario | `#1a2456` | barra de aviso, botones primarios, panel del hero, footer, acentos |
| Azul de interacción | `#2f5bff` | hover de botones primarios, enlaces, foco |
| Tinta | `#14171f` | texto principal |
| Tinta secundaria | `#4a5163` | párrafos |
| Tinta tenue | `#6b7288` | etiquetas, metadatos |
| Tinta muy tenue | `#9aa1b4` | SKU, precios tachados |
| Fondo | `#ffffff` | página |
| Superficie | `#f5f6f9` | tarjetas de imagen, paneles de formulario, hero izquierdo |
| Superficie alterna | `#fafbfd` | cabeceras de tabla, franja de beneficios |
| Borde | `#e6e8ef` | divisores y bordes de tarjeta |
| Borde de control | `#d9dce6` | inputs, selects, chips |
| Naranja acento | `#f26722` | etiquetas de descuento, detalle en ilustraciones |
| Verde stock | `#1f7a3d` | "en stock", descuentos aplicados |
| Ámbar stock bajo | `#b06a00` | "últimas N unidades" |
| Rojo alerta | `#c62828` | sin stock, validación, anulado |
| Fondo estado ok | `#eaf6ee` | chip "Entregado" |
| Fondo estado alerta | `#fdecec` | chip "Anulado" |
| Fondo estado activo | `#eef1fb` | chip "En preparación", tinta sobre azul marino |

App móvil, además: tema oscuro con fondo `#0d1017`, superficie `#191d27`, tinta `#eef0f6`, acento `#6d8bff`.

### Tipografía

Familia única: **Archivo** (sans-serif). Fallback: system-ui, sans-serif.

| Rol | Tamaño | Peso | Tracking |
| --- | --- | --- | --- |
| Hero H1 | 54px (desktop) / 42px (tablet) / 34px (móvil) | 800 | −0.045em |
| H1 de página | 40px / 34px / 28px | 800 | −0.045em |
| H2 sección | 32px | 800 | −0.04em |
| Precio destacado | 22–28px | 800 | −0.04em |
| Nombre de producto | 15px | 800 | −0.015em |
| Cuerpo | 15px / 1.55 | 400 | 0 |
| Cuerpo secundario | 13.5px | 400–600 | 0 |
| Metadato | 12.5px | 600 | 0 |
| Etiqueta versal | 10–11px | 800 | 0.14–0.24em, mayúsculas |
| SKU | 10px | 600 | 0.08–0.12em |

Todo número monetario o de cantidad usa `font-variant-numeric: tabular-nums`.

### Espaciado, radios, sombras

- Escala de espaciado: 4, 6, 8, 12, 14, 16, 18, 20, 24, 26, 30, 32, 40, 56, 64, 72, 88px.
- Radio: 4px (chips y etiquetas), 6px (botones, inputs, chips grandes), 8px (miniaturas), 10px (tarjetas, paneles), 12px (tarjeta de confirmación), 9–13px (píldoras y switches).
- Sombra: solo dos usos — hover de tarjeta de producto `0 12px 28px rgba(20,23,31,.1)` y toast `0 12px 30px rgba(20,23,31,.25)`.
- Ancho de contenido: `max-width: 1300px` centrado; el documento se limita a `1440px` en escritorio.

### Movimiento

| Nombre | Duración | Curva | Uso |
| --- | --- | --- | --- |
| `w-float` | 6–7s infinito | ease-in-out | flotado suave de las imágenes del hero (±10px) |
| `w-in` | 0.2–0.5s | ease | entrada de bloques (opacidad + 12–16px) |
| Elevación de botón | 0.16s | cubic-bezier(.34,1.5,.64,1) | hover: `translateY(-2px)` |
| Presionado | 0.12s | ease | `scale(.96–.98)` |
| Cambio de color | 0.2s | ease | fondo, borde, texto |
| Switch | 0.2s | cubic-bezier(.34,1.4,.64,1) | desplazamiento del pomo |
| Intro de marca | 3s | ease | ver "Intro" |

Todo se anula bajo `prefers-reduced-motion: reduce`.

## Intro de marca (web)

Cortina fija a pantalla completa sobre todo el contenido, fondo `#1a2456`, durante 3 segundos:

1. Rayo blanco (84×112px) entra con `scale(.86 → 1)` y opacidad 0 → 1 en el primer 30% del tiempo.
2. El mismo rayo se ilumina: `drop-shadow` de 0 a `0 0 26px rgba(255,255,255,.95)` al 42%, baja a 8px al 52%, y queda en 22px desde el 64%. La opacidad acompaña: 0.35 → 1 → 0.85 → 1.
3. "NOVA" (30px, peso 800, blanco) aparece entre el 40% y el 70%, con el tracking cerrándose de 0.4em a 0.08em.
4. "GENERAL ELECTRIC" (11px, peso 700, tracking 0.34em, mayúsculas, opacidad 0.75) aparece a partir del 58%.
5. Del 72% al 100% la cortina se desvanece a opacidad 0 y `visibility: hidden`; el estado `intro` pasa a false a los 3000ms.

La cortina no captura eventos (`pointer-events: none`).

## Screens / Views — Web

### 1. Header global (en todas las vistas)

- **Barra de aviso**: fondo `#1a2456`, texto blanco 12.5px peso 600, tracking 0.06em, centrado, padding 9px 24px. Copy: "Envío gratis en compras sobre $80.000 · Retiro en tienda en 2 horas".
- **Fila principal**: fondo blanco, borde inferior 1px `#e6e8ef`, padding 20px 24px, contenido a 1300px.
  - **Logo**: cuadrado 38px, radio 6px, fondo `#1a2456`, rayo blanco centrado. A la derecha "NOVA" (19px, 800, tracking −0.035em) y "General Electric" (8px, 700, tracking 0.2em, mayúsculas, `#6b7288`).
  - **Buscador**: contenedor flexible hasta 640px, borde 1px `#d9dce6`, radio 6px, hover borde `#1a2456`. Dentro: select de colección (fondo `#f5f6f9`, 13px peso 700, borde derecho 1px), input ("Buscar productos, marcas o códigos…", 14px) y botón de lupa 48×44px fondo `#1a2456`, hover `#2f5bff`.
  - **Mi cuenta**: icono `user-round` 20px + etiqueta doble ("Mi cuenta" 10px `#6b7288` / "Ingresar" 13px peso 700). Con sesión abierta la segunda línea pasa a "Rodrigo P.". Hover: fondo `#f2f4f8`, radio 6px.
  - **Carrito**: icono `shopping-cart` 20px con globo de conteo anclado al icono (arriba −8px, derecha −10px; mínimo 18px, radio 9px, fondo azul marino, texto blanco 10.5px peso 800). Etiqueta doble ("Carrito" / total en CLP).
- **Navegación**: borde superior 1px, ocho ítems (Inicio, Cables, Iluminación, Protección, Interruptores, Herramientas, Ofertas, Contacto), padding 15px 16px, 13.5px peso 700. Activo: texto `#1a2456` y borde inferior 2px `#1a2456`. Inactivo: `#4a5163`, hover `#1a2456`.

### 2. Home

- **Hero**: grid de dos columnas 65% / 35%, misma altura, sin separación, mínimo 520px.
  - *Izquierda*: fondo `#f5f6f9`, padding 64px 56px 64px 72px, grid interno de dos columnas. Bloque de texto: kicker "NOVA GENERAL ELECTRIC" (11px, 800, tracking 0.24em, `#6b7288`), H1 "Materiales / eléctricos / certificados" (54px, 800, −0.045em, tres líneas), párrafo 16px `#4a5163` máx. 40ch, botón primario "Comprar ahora" con flecha (padding 16px 26px, fondo `#1a2456`, radio 6px, 14.5px peso 800). A su derecha, ilustración de 420px de alto con flotado.
  - *Derecha*: fondo `#1a2456`, padding 44px 48px 48px. Ilustración en tinta clara `#eef1fb` posicionada arriba (260px de alto, flotado). Debajo: etiqueta "−22% ESTA SEMANA" (fondo blanco, texto `#1a2456`, radio 4px, 11px peso 800), H2 "Cables THHN por rollo" (30px, 800, blanco) y botón blanco "Ver la oferta" con texto `#14171f`.
- **Categorías**: cabecera con kicker + H2 "Todo para la instalación" y botón contorneado "Ver catálogo completo". Debajo, grid de 7 tarjetas (gap 16px), cada una 230px de alto, fondo `#f5f6f9`, radio 10px: nombre en **texto vertical** pegado al borde izquierdo (`writing-mode: vertical-rl` rotado 180°, 12px, 800, tracking 0.14em, mayúsculas, azul marino), ilustración centrada a la derecha del texto, y conteo de SKU abajo a la derecha (10.5px, `#6b7288`). Hover: `translateY(-4px)`, borde `#1a2456`, fondo `#eef0f6`.
- **Beneficios**: franja `#fafbfd` con borde superior, cuatro columnas, cada una con icono 22px azul marino + título 14px peso 800 + descripción 12.5px `#6b7288`: despacho mismo día, retiro en 2 horas, producto certificado SEC, boleta o factura.
- **Footer**: fondo `#1a2456`, texto `#c9cfe4` 12.5px centrado: razón social, dirección y correo.

### 3. Catálogo por categoría

- Migaja "Inicio › <categoría>".
- Cabecera: H1 con el título de la categoría (40px) y bajada de hasta 62ch; a la derecha, conteo de resultados y select de orden (Relevancia, precio ascendente, precio descendente, mayor descuento, mayor stock).
- Grid de dos columnas 236px / 1fr, gap 40px:
  - *Barra lateral*: lista de las 7 categorías (activa con borde izquierdo 2px azul marino y peso 800, cada fila con su conteo), chips de marca (activo: fondo azul marino, texto blanco), y dos interruptores en forma de botón ("Solo con stock", "Solo ofertas") más "Limpiar filtros".
  - *Grid de productos*: tres columnas, gap 20px. Tarjeta: borde 1px `#e6e8ef`, radio 10px, imagen de 190px sobre `#f5f6f9`, etiqueta de descuento naranja arriba a la izquierda, etiqueta "Agotado" (fondo `#14171f`) arriba a la derecha, marca y SKU en una línea, nombre 15px peso 800, especificación 12.5px, estado de stock con color según nivel, precio anterior tachado, precio 22px peso 800, unidad, y botón "Agregar" azul marino con icono `plus`. Hover de tarjeta: `translateY(-4px)` + sombra + borde `#c9cfe4`.
- **Estado vacío**: panel `#fafbfd` con icono `filter-x`, título "Ningún producto cumple los filtros", explicación y botón "Limpiar filtros".

### 4. Carrito y checkout

Grid 1fr / 380px.

- **Líneas**: contenedor con borde y radio 10px. Cada línea: miniatura 82px, marca y SKU, nombre, precio unitario con unidad, control de cantidad (menos / valor / más, borde 1px, radio 6px, botones 36px) y "Quitar"; a la derecha el total de línea (19px peso 800). Al superar el stock disponible aparece un aviso "Stock máximo: N".
- **Entrega**: dos opciones tipo radio (círculo 18px con punto 9px): "Retiro en tienda · Listo en 2 horas · Av. Matta 1240" (Gratis) y "Envío a obra · Mismo día si compras antes de 14:00" ($4.990, gratis sobre $80.000 netos). Seleccionada: fondo `#f2f4f8`, borde `#1a2456`.
- **Método de pago**: dos opciones — "Transferencia bancaria · 3% de descuento · adjunta comprobante" y "Pago en tienda · Efectivo o tarjeta al retirar". (Los métodos de tarjeta en línea y crédito empresa fueron retirados a pedido del cliente.)
  - Transferencia: panel con datos bancarios (razón social, RUT, banco, cuenta, correo) y botón "Adjuntar comprobante (foto o PDF)" que **abre el selector de archivos del dispositivo** (`accept="image/*,application/pdf"`). Con archivo cargado: fila `#fafbfd` con miniatura real de la imagen (o icono `file-text` si es PDF), nombre truncado a 34 caracteres, peso en KB, "listo para enviar" y botón "Quitar" (hover rojo). La miniatura se genera con `URL.createObjectURL` y se libera al quitar el archivo.
  - Pago en tienda: nota de reserva por 24 horas.
- **Cupón**: input en mayúsculas + botón "Aplicar". Código válido: `NOVA5` → 5% de descuento. Cualquier otro muestra "Cupón no válido".
- **Resumen** (columna derecha): subtotal, descuento por transferencia (3%, en verde), cupón (en verde), IVA 19%, despacho, y total en 28px peso 800. Botón de pago a ancho completo cuyo texto depende del método ("Confirmar transferencia" / "Reservar pedido"). Sin comprobante adjunto el envío se bloquea y aparece "Falta adjuntar el comprobante" en rojo con icono de alerta.
- **Estado vacío**: panel con icono de carrito, "El carrito está vacío" y botón "Ir al catálogo".

### 5. Confirmación

Tarjeta de 820px centrada, radio 12px: cabecera azul marino con icono `check-check`, "Pedido confirmado" (34px) y "Orden #NNNN · N ítems"; filas de pago y entrega; total pagado en 28px. Debajo, "Seguir comprando" (primario) y "Ver mis pedidos" (contorneado). Al navegar a otra vista el recibo se descarta.

### 6. Ingreso / registro

Dos columnas. Izquierda: kicker "Mi cuenta", H1 "Compra con precio de instalador", párrafo y tres beneficios con icono (repetir pedidos, boleta o factura automática, aviso de reposición). Derecha: panel `#f5f6f9` radio 10px con conmutador de dos pestañas ("Ya tengo cuenta" / "Crear cuenta"), campos (nombre y RUT solo en registro; correo; contraseña), enlace "¿Olvidaste tu contraseña?" solo en ingreso, botón "Continuar" y nota con candado.

### 7. Mi cuenta

- Cabecera: avatar cuadrado 56px radio 8px con iniciales sobre azul marino, nombre 28px, metadatos (patente SEC, RUT, correo) y botón "Cerrar sesión".
- Tres tarjetas de estadística `#f5f6f9`: pedidos del año, gasto del mes, ahorro en ofertas (valor 26px peso 800).
- Grid 236px / 1fr. Barra lateral con cuatro secciones (Mis pedidos, Direcciones, Facturación, Preferencias), la activa con fondo `#f2f4f8` y borde izquierdo 2px.
  - *Mis pedidos*: tabla con cabecera `#fafbfd` y columnas 1.1fr / 1.2fr / 1fr / 0.9fr / 28px — pedido y cantidad de ítems, fecha, estado como chip de color, total, y chevron. Fila con hover `#f7f8fb`, abre el detalle.
  - *Direcciones*: dos tarjetas seleccionables con icono, nombre, detalle y chip "Predeterminada"; botón con borde discontinuo "Agregar dirección".
  - *Facturación*: conmutador Boleta / Factura electrónica; al elegir factura aparece panel con los datos tributarios.
  - *Preferencias*: dos filas con switch (aviso de reposición de stock, ofertas semanales).

### 8. Detalle de pedido

Enlace "‹ Mis pedidos", H1 "Pedido #NNNN" con el estado a la derecha, y una barra de progreso de cuatro pasos (Recibido, En preparación, En ruta, Entregado): barra de 5px radio 3px en azul marino para los pasos alcanzados y `#e6e8ef` para los pendientes, etiqueta 11.5px en mayúsculas, opacidad 0.55 en los no alcanzados. Debajo, grid 1fr / 320px: líneas del pedido (miniatura 64px, cantidad, nombre, marca y SKU, total) y resumen lateral (fecha, entrega, pago, neto, IVA, total) con botón "Repetir este pedido" que carga las líneas al carrito.

### 9. Contacto

Dos columnas: datos (dirección con horario, teléfono con WhatsApp, correo) y formulario `#f5f6f9` con nombre o empresa, correo, detalle de materiales y botón "Enviar solicitud".

## Screens / Views — App móvil

Marco de 468px de ancho con barra de estado simulada, cabecera propia y barra de pestañas fija de cinco ítems (Inicio, Catálogo, Buscar, Carrito, Cuenta). El estilo es más rectilíneo que la web: sin radios, reglas de 2px, líneas punteadas, códigos en monoespaciada, y motivo de boleta.

- **Home**: banner de oferta con cuenta regresiva viva y código de barras dibujado, cinco categorías en rejilla, carrusel "Comprar de nuevo" con repetición de pedido en un toque, y grilla de destacados con esqueletos de carga.
- **Catálogo**: barra de filtros y orden, chips de categoría, hoja inferior de filtros (categorías, marcas, precio máximo con deslizador, tres interruptores) que muestra "Ver N productos" antes de aplicar, y alternancia entre vista de grilla y lista.
- **Buscar**: escáner de código simulado a pantalla completa con mira y barrido, historial editable, búsquedas frecuentes, búsqueda por especificación (amperaje, calibre, luz, seguridad) y **calce de lista de materiales**: se pega un listado con cantidades, la app lo cruza contra el catálogo, marca las líneas sin coincidencia y arma el carrito.
- **Carrito**: líneas con control de cantidad, entrega, método de pago (transferencia con comprobante, pago en tienda), cupón, resumen con IVA y sello animado "AGREGADO" al sumar productos.
- **Cuenta**: perfil, estadísticas, pedidos, direcciones, documento tributario, preferencias y modo oscuro.

Búsqueda con tolerancia a errores de tipeo en ambas superficies: normaliza acentos, unifica "2x20" y "2×20", separa en palabras y acepta hasta 2 caracteres de diferencia según el largo del término. "cabel", "ampoyeta" o "automatico" encuentran resultados.

## Interactions & Behavior

- **Navegación**: no hay rutas; una variable de vista decide qué pantalla se muestra. Cada cambio de vista reinicia filtros, cierra el detalle de pedido y descarta el recibo, y lleva el scroll al inicio.
- **Agregar al carrito**: suma una unidad; si ya existe la línea incrementa la cantidad. Sin stock no agrega y avisa "Te avisamos cuando llegue <SKU>".
- **Cantidades**: bajar a 0 elimina la línea. Subir por sobre el stock disponible se rechaza con aviso.
- **Filtros**: categoría (una a la vez desde los chips, varias desde la hoja móvil), marcas (varias), solo con stock, solo ofertas, precio máximo (móvil). "Ofertas" en el menú equivale a filtrar por descuento y ordenar por mayor descuento.
- **Cálculo del total**: subtotal → descuento por transferencia (3%) → cupón (5%) → neto; IVA 19% sobre el neto; despacho 0 en retiro, 0 sobre $80.000 netos, $4.990 en el resto; total = neto + IVA + despacho.
- **Bloqueo de pago**: con transferencia elegida y sin comprobante adjunto, el botón no envía y muestra el aviso en rojo.
- **Toast**: mensaje inferior centrado, fondo `#14171f`, 2.2 segundos, sin capturar eventos.
- **Responsive**: tres tramos por ancho de ventana — móvil bajo 720px, tablet entre 720 y 1080px, escritorio sobre 1080px. En móvil: hero de una columna, grid de productos de una columna, categorías en dos columnas, barra lateral convertida en fila de chips, buscador movido bajo la fila del header, etiquetas del header ocultas, tabla de pedidos reducida a dos columnas. En tablet: hero 58/42, grid de dos columnas, categorías en cuatro, barra lateral horizontal.

## State Management

Estado por superficie:

- `view` — pantalla activa.
- `query`, `collection` — búsqueda.
- `lines: [{sku, qty}]` — carrito, única fuente del conteo y del total del header.
- `brands: []`, `sort`, `onlyStock`, `onlyOffer` — filtros del catálogo.
- `ship` (`pickup` | `delivery`), `pay` (`transfer` | `cash`).
- `receipt`, `receiptName`, `receiptSize`, `receiptUrl`, `receiptIsImg` — comprobante adjunto.
- `coupon`, `couponOk`.
- `placed`, `done` — número de orden y copia inmutable del recibo.
- `signedIn`, `authMode`, `acctTab`, `acctOrder`, `addr`, `docType`, `notifStock`, `notifOffers`.
- `intro` — cortina de marca, pasa a false a los 3000ms.

En la app móvil se añaden `theme` (claro/oscuro), `history`, `bom`, `bomRun`, `scan`, `scanHit`, y el estado de la hoja de filtros con borrador (`draft`) que solo se aplica al confirmar.

**Datos**: `catalogo.json` se carga al montar (`fetch`, sin caché) y reemplaza el catálogo de respaldo incluido en el archivo. Estructura: `{ currency, categories: [{key, label, count, title, lead}], products: [{sku, cat, brand, name, spec, price, old, stock, unit}] }`. `old` en 0 significa sin oferta. Este archivo es el contrato natural con la API real: reemplázalo por el endpoint del backend sin cambiar la interfaz.

Nada persiste entre sesiones. No hay autenticación, pagos ni inventario reales.

## Assets

- **Iconos**: Lucide (https://lucide.dev), grosor 1.4–2.6 según contexto. Usados: search, user-round, shopping-cart, plus, minus, arrow-right, arrow-left, chevron-right, chevron-down, check, check-check, x, truck, store, shield-check, receipt, building-2, upload, file-text, lock, map-pin, phone, mail, package, settings, log-out, bell, rotate-ccw, hard-hat, wrench, filter-x, alert-triangle, sliders-horizontal, scan-line, hash, history, corner-down-left, clipboard-list, wand-sparkles, camera, contrast, layout-grid, list, cable, lightbulb, toggle-right, route, gauge, screwdriver, box, plug.
- **Tipografía**: Archivo, provista por el sistema de diseño Modernist.
- **Ilustraciones de producto**: SVG planos dibujados a mano por familia (rollo de cable, ampolleta, automático, placa de interruptor, herramienta, canaleta, instrumento de medición), en trazo azul marino con detalle naranja, sobre fondo transparente y ajustadas sin recorte. **Son material de relleno, no fotografía de producto.** El cliente debe reemplazarlas por fotos propias o por los packs de imágenes de sus proveedores (Electrocables, Schneider, Bticino, Veto). No se usó fotografía de stock: las fuentes públicas probadas dieron resultados irrelevantes o con bordes de relleno.
- **Logo**: rayo blanco sobre cuadrado azul marino, dibujado en SVG. Es un logo genérico de trabajo, no una marca registrada.

## Design system

Ambas superficies se construyeron sobre el sistema **Modernist** (Archivo, rejilla modular, reglas fuertes), con una desviación deliberada en la web: se introdujo radio de 6–12px en botones y tarjetas para acercarse al referente de e-commerce que pidió el cliente. La app móvil conserva el radio 0 del sistema. Si el codebase destino tiene su propio sistema, prioriza el suyo y conserva de aquí la paleta y la jerarquía tipográfica.

## Files

| Archivo | Contenido |
| --- | --- |
| `NOVA Web Home.dc.html` | tienda web completa: home, catálogo, carrito, cuenta, contacto, intro de marca |
| `NOVA General Electric.dc.html` | app móvil completa |
| `catalogo.json` | 38 productos y 7 categorías |
| `NOVA-General-Electric-web.html` | web empaquetada en un solo archivo, abre sin dependencias |
| `Voltio Home.dc.html` | exploración previa descartada, otra identidad; solo referencia histórica |

Los archivos `.dc.html` abren directo en el navegador. Para revisarlos usa el archivo empaquetado, que no necesita servidor.

## Pendientes conocidos

- Falta conectar la app móvil a `catalogo.json`; hoy tiene su propia copia de los datos.
- La moneda es CLP; el cliente mencionó un proveedor ecuatoriano, así que conviene confirmar mercado antes de implementar.
- Fotografía de producto pendiente de entrega por el cliente.
- Sin ficha de producto individual: las tarjetas agregan al carrito directamente.
