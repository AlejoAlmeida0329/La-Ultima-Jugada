# 03_VOICE — La Última Jugada

> Sistema de voz, tono y copy. Cargar siempre que se trabaje en texto público: home, PDP, checkout, emails, redes, soporte, errores.

---

## Esencia de voz

**Hablamos como un amigo que sabe de fútbol y no te vende humo.**

Directos. Con conocimiento. Sin floritura. Sin servilismo. Honestos hasta cuando es incómodo (sí, somos réplicas y lo decimos).

---

## Pilares de voz

### 1. Directa
Vamos al punto. Sin "estimados clientes", sin "nos complace anunciar". Si se puede decir en 4 palabras, no lo decimos en 12.

### 2. Con conocimiento
Sabemos de fútbol. Sabemos de telas, de fits, de modelos. No usamos lenguaje aspiracional vacío. Hablamos como alguien que está adentro.

### 3. Con actitud
No somos servil ni mendigantes. No suplicamos compras. No usamos exclamaciones múltiples. Tenemos lo que queremos vender y lo presentamos bien.

### 4. Honesta
Réplicas, lo decimos. Sin stock, lo decimos. Demora de envío, lo decimos. La honestidad es la diferencia con el revendedor de WhatsApp.

---

## Decisión de tratamiento

**Tuteo neutro colombiano** por defecto.

- Sí: "Elige tu talla", "Mira la nueva colección"
- No (voseo): "Elegí tu talla", "Mirá la nueva colección"
- No (usted): "Seleccione su talla"

**Excepción:** documentos legales (política de privacidad, términos) en "usted" formal, por convención del sector.

---

## Reglas duras

1. **Sin emojis** en copy comercial. (Emojis en redes sociales: con criterio, no decorativos.)
2. **Sin exclamaciones múltiples.** Una sola, y solo cuando aporta. Por defecto, ninguna.
3. **Sin frases en inglés mal traducidas.** Nada de "shop now", "new drop", "limited edition". En español, directo.
4. **Sin lenguaje inclusivo forzado.** Nada de "amig@s", "tod@s", "x". Si necesitamos hablar a un grupo, lo hacemos con sustantivos colectivos: "la gente", "ustedes", "el equipo".
5. **CTAs en mayúsculas.** Verbo + objeto, máximo 3 palabras.
6. **Sin "click aquí" / "haz click".** Usamos verbos específicos.
7. **Sin "querido cliente" ni "estimado usuario".** Hablamos con personas, no con avatares.
8. **Sin "lo sentimos" en errores triviales.** Reservamos las disculpas para cuando realmente la cagamos.
9. **Sin frases motivacionales.** Nada de "tu mejor versión", "supera tus límites", "el límite eres tú".

---

## Patrones por componente

### Home — Hero

- **Headline:** 3–7 palabras. Contundente. Verbo o sustantivo fuerte.
- **Subhead:** 1 línea. Explica, no adorna.
- **CTA:** 2–3 palabras en mayúsculas.

**Ejemplo bueno:**
> **Tricolor 25/26.**
> La nueva. Réplica premium calidad 1:1.
> **VER COLECCIÓN**

**Ejemplo malo:**
> **¡Descubre la increíble nueva colección oficial de la selección Colombia 25/26!**
> *No vuelvas a perderte de la oportunidad de lucir como un campeón.*
> **¡COMPRA AHORA!**

---

### Product Card (catálogo)

Estructura:
1. Imagen
2. Name + Subtitle
3. Precio
4. (opcional) Tag de estado: "Nuevo", "Sin stock", "Últimas tallas"

Sin descripciones largas. Sin promesas. El producto se vende solo en el catálogo.

---

### PDP (Product Detail Page)

Orden de información:
1. **Galería de imágenes** (izquierda en desktop, arriba en móvil)
2. **Name** (display, grande)
3. **Subtitle** (gris cemento)
4. **Precio**
5. **Selector de talla** + "¿Cuál es mi talla?" (link a guía)
6. **Botón:** AGREGAR AL CARRITO
7. **Disclaimer corto:** "Réplica premium calidad 1:1"
8. **Descripción corta** (2–3 líneas)
9. **Descripción larga** (acordeón)
10. **Especificaciones técnicas** (tabla)
11. **Política de devoluciones** (link)
12. **Productos relacionados**

**Descripción corta — patrón:**
> Camiseta réplica premium calidad 1:1, estilo selección Colombia local 25/26. Poliéster reciclado. Transpirable. Escudo bordado.

---

### Checkout

- Labels claros y cortos: "Correo", "Nombre", "Dirección", "Ciudad", "Teléfono"
- No "Por favor ingrese su...". Solo el label.
- Placeholder solo para formato: "ejemplo@correo.com"
- Botones de avance: **CONTINUAR** / **PAGAR $130.000**
- En el botón final mostramos el monto exacto.

---

### Estados vacíos

Sin "Lo sentimos". Con salida.

| Caso | Copy |
|---|---|
| Sin resultados de búsqueda | "Nada por acá. Probá otro filtro." |
| Carrito vacío | "Carrito vacío. Volvé a la tienda." |
| Sin órdenes en mi cuenta | "Todavía no hay órdenes. Cuando compres, aparecen acá." |
| Sin productos en colección | "Esta colección está vacía por ahora." |

---

### Errores

Específicos. Sin culpar. Con acción clara.

| Caso | Copy |
|---|---|
| Email mal formado | "Ese correo no se ve bien. Revísalo." |
| Tarjeta rechazada | "El banco no autorizó el pago. Intenta otra tarjeta o PSE." |
| Talla no seleccionada | "Te falta elegir talla." |
| Stock agotado en checkout | "Justo se acabó esa talla. ¿Probás otra?" |
| 404 | "Esa jugada no existe. Volvé al inicio." |
| 500 | "Algo se rompió de nuestro lado. Intentá en un minuto." |

---

### Notificaciones (toast / inline)

| Caso | Copy |
|---|---|
| Producto agregado | "Listo. En el carrito." |
| Login | "Bienvenido de vuelta." |
| Logout | "Hasta la próxima." |
| Cupón aplicado | "Cupón activo. -$20.000" |
| Cupón inválido | "Ese cupón no sirve acá." |

---

### Estados de orden

| Estado | Copy al cliente |
|---|---|
| Pendiente de pago | "Esperando confirmación de pago." |
| Pagada | "Pagada. Preparando tu pedido." |
| En preparación | "Empacando." |
| Despachada | "En camino. Acá va tu tracking." |
| Entregada | "Listo. Llegó." |
| Cancelada | "Orden cancelada. Reembolso en proceso." |

---

## Emails transaccionales

### Confirmación de orden
- **Asunto:** Tu orden #{ID} está en marcha
- **Cuerpo:** Resumen de productos, total, dirección, tiempo estimado. Sin floritura.

### Envío en camino
- **Asunto:** Tu pedido salió
- **Cuerpo:** Tracking, transportadora, fecha estimada.

### Entregado
- **Asunto:** Llegó tu pedido
- **Cuerpo:** Confirmación, link para devoluciones si aplica, link para reseña en H2+.

### Carrito abandonado (mes 2+)
- **Asunto:** Dejaste algo en el campo
- **Cuerpo:** Producto + CTA "Termina la jugada".

### Restock de tu talla
- **Asunto:** Volvió tu talla
- **Cuerpo:** Producto + CTA.

---

## Microcopy de botones

| Acción | Texto |
|---|---|
| Comprar | AGREGAR AL CARRITO |
| Ir al carrito | VER CARRITO |
| Avanzar checkout | CONTINUAR |
| Pagar | PAGAR ${MONTO} |
| Volver | VOLVER |
| Seguir comprando | SEGUIR COMPRANDO |
| Ver más | VER MÁS |
| Suscribirse a alerta | AVÍSAME |
| Confirmar acción | CONFIRMAR |
| Cancelar acción | CANCELAR |

Nunca: "Click aquí", "Siguiente", "OK", "Submit".

---

## Frases canónicas (manifiesto)

Para banners, packaging, redes, about, signature de email.

- "La jugada que define el partido."
- "Sin pretextos."
- "Vistes lo que juegas."
- "Para el que está en el campo, no para el que mira."
- "Réplica premium. Sin disfraces."

---

## Do / Don't — ejemplos lado a lado

| Contexto | ❌ Don't | ✅ Do |
|---|---|---|
| Headline producto | "Increíble camiseta oficial de la selección Colombia" | "Tricolor 25/26. Local. Réplica premium." |
| CTA principal | "¡Haz click aquí para comprar ya!" | "AGREGAR AL CARRITO" |
| Estado vacío | "Lo sentimos, no se encontraron resultados." | "Nada por acá. Probá otro filtro." |
| Error de form | "Por favor ingrese un correo electrónico válido." | "Ese correo no se ve bien. Revísalo." |
| Confirmación | "¡Felicidades! Tu compra fue procesada exitosamente." | "Listo. Orden confirmada. Te llega correo en 1 minuto." |
| Carrito vacío | "Tu carrito está vacío. ¡Empieza a comprar ahora!" | "Carrito vacío. Volvé a la tienda." |
| Página 404 | "Error 404: Página no encontrada" | "Esa jugada no existe. Volvé al inicio." |
| Newsletter | "¡Suscríbete y recibe ofertas exclusivas!" | "Drops nuevos antes que todos. Un correo al mes." |
| Footer redes | "Síguenos en nuestras redes sociales" | "Seguinos." |
| Talla agotada | "Lo sentimos, este producto se encuentra agotado." | "Sin stock. Avísame cuando vuelva." |
| About | "Somos una empresa dedicada a la venta de..." | "Vendemos lo que vestiríamos." |
| Disclaimer réplica | "Aviso legal: nuestros productos son réplicas no oficiales..." | "Réplica premium calidad 1:1. No es producto oficial. Lo decimos claro." |
| Promoción | "¡Aprovecha esta increíble oferta limitada por tiempo limitado!" | "20% off hasta el domingo." |
| Llamado a ver colección | "Descubre nuestra increíble nueva colección" | "Mira la nueva." |
| Soporte | "¿En qué podemos ayudarte el día de hoy?" | "¿Qué necesitas?" |
| Bienvenida email | "¡Bienvenido a la familia La Última Jugada!" | "Estás dentro. Acá lo que viene." |
| Producto agotado en checkout | "Lo sentimos, este producto ya no se encuentra disponible." | "Justo se acabó. ¿Probás otra talla?" |
| Confirmación devolución | "Hemos recibido su solicitud de devolución y será procesada en breve." | "Recibimos tu devolución. Reembolso en 7 días hábiles." |

---

## Estructura de manifiesto largo (para about / packaging)

Si necesitamos texto largo de marca (página *Sobre*, tarjeta de empaque, post de lanzamiento), usar este patrón:

1. **Afirmación inicial** — 1 frase fuerte.
2. **Lo que no somos** — 2–3 cosas que rechazamos.
3. **Lo que sí somos** — 2–3 cosas que defendemos.
4. **Cierre** — 1 frase con verbo.

**Ejemplo:**

> La Última Jugada es la camiseta del que entiende.
>
> No somos San Andresito. No somos el revendedor de WhatsApp. No somos la imitación barata.
>
> Somos réplica premium calidad 1:1. Somos catálogo curado. Somos la marca del que vive el deporte adentro, no afuera.
>
> Vistes lo que juegas.

---

## Reglas para copywriter futuro

Cuando contrates copywriter freelance o agencia:

1. Entregale este documento + `02_BRAND.md` antes que cualquier brief.
2. Pedile que escriba 3 ejemplos por componente antes de aprobar el contrato (prueba de voz).
3. Hacé feedback con referencia al doc: "Esto rompe la regla X", no "no me gusta".
4. Mantené un changelog de frases aprobadas — se vuelven banco para campañas futuras.
