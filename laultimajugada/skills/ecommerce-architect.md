# Skill: ecommerce-architect

> Cómo estructurar flujos, páginas y lógica de negocio de un e-commerce funcional.

---

## Cuándo activar este skill

- Diseñar el flujo de compra (de catálogo a confirmación)
- Estructurar PDPs, carrito, checkout
- Definir lógica de stock, precios, cupones, envíos
- Construir el sitemap o navegación
- Resolver edge cases de comercio (oversell, devoluciones, fraudes)
- Diseñar funnels y trackeo de conversión

## Contexto necesario

Cargar siempre junto:
- `01_PRD.md` (requerimientos, reglas de negocio)
- `06_CATALOGO.md` (modelo de datos)

---

## Principios duros

1. **Mobile-first siempre.** El 80% del tráfico colombiano de e-commerce es móvil. Diseño base 360px.
2. **Checkout en 1 página, 3 pasos visuales máximo.** Contacto → Envío → Pago. Sin pasos extra.
3. **Guest checkout funcional.** No obligamos a crear cuenta para comprar.
4. **Carrito persistente.** Sobrevive a refresh y entre sesiones (localStorage + DB si está logueado).
5. **Performance LCP < 2.5s en móvil 4G.** Las imágenes pesadas matan conversión.
6. **Stock decremento al pagar confirmado**, no al meter al carrito. Riesgo de oversell aceptado en H1 por volumen bajo.

## Estructura estándar de PDP

Orden vertical en móvil, dos columnas en desktop (galería izq, info der):

1. Galería (carrusel táctil en móvil)
2. Name (display grande)
3. Subtitle (gris cemento)
4. Precio (display, prominente)
5. Selector de talla (chips o dropdown) + link "¿Cuál es mi talla?"
6. CTA principal — AGREGAR AL CARRITO
7. Disclaimer corto — "Réplica premium calidad 1:1"
8. Descripción corta (2–3 líneas)
9. Acordeón: descripción larga
10. Acordeón: especificaciones técnicas
11. Link a política de devoluciones
12. Productos relacionados (de la misma colección)

## Funnel de conversión esperado

```
Landing / Home          100%
  ↓
Vista de catálogo        60%
  ↓
PDP                      30%
  ↓
Add to cart              10%
  ↓
Inicio checkout           5%
  ↓
Compra confirmada      2-3%   ← objetivo
```

Cada paso debe tener trackeo en PostHog. Si un paso cae más del 50% respecto al esperado, es señal de problema.

## Flujo de checkout (1 página, 3 pasos)

### Paso 1 — Contacto
- Correo (con autosave para abandono)
- Teléfono

### Paso 2 — Envío
- Nombre completo
- Cédula
- Dirección línea 1
- Dirección línea 2 (opcional)
- Ciudad
- Departamento (dropdown)
- Código postal (opcional)
- Notas de entrega (opcional)
- Mostrar costo de envío fijo: $12.000

### Paso 3 — Pago
- Selector de método: tarjeta / PSE / Tikin
- Resumen del pedido visible (productos, subtotal, envío, total)
- Aceptación de términos (checkbox)
- Botón: PAGAR ${TOTAL}

### Post-checkout
- Página de confirmación con número de orden
- Email automático en menos de 1 minuto
- CTA para crear cuenta (opcional, no forzado)

## Estados de orden

```
pending_payment → paid → preparing → shipped → delivered
                  ↓
              cancelled (refund_in_progress → refunded)
```

Cada cambio de estado dispara email transaccional al cliente.

## Lógica de carrito

- Persistente entre sesiones (localStorage + DB si logueado)
- Validación de stock al cargar el carrito (no en cada vista)
- Si una variante quedó sin stock mientras estaba en carrito → mostrar warning, no eliminar automáticamente
- Botón "Limpiar carrito" con confirmación

## Lógica de cupones

- Aplican a nivel de carrito (no por producto en H1)
- Tipos: porcentaje (%) o monto fijo
- Pueden tener: fecha de expiración, monto mínimo de carrito, límite de usos totales, límite de usos por usuario
- Si un cupón no aplica: mostrar razón específica ("Necesita mínimo $X", "Expirado", "Ya lo usaste")

## Manejo de stock

- Validación en 3 momentos: al agregar al carrito, al iniciar checkout, al confirmar pago
- Si stock cae a 0 entre agregar y pagar: bloquear pago y notificar
- Producto con stock 0: visible pero CTA cambia a "AVÍSAME" con captura de email

## SEO básico

- URLs limpias: `/producto/[slug]`, `/coleccion/[slug]`
- Meta title y description por producto (configurables en admin)
- Sitemap.xml autogenerado
- Robots.txt
- Schema.org Product en PDP (JSON-LD)
- OpenGraph y Twitter cards
- Sin marcas registradas en ningún meta

## Edge cases que tenés que resolver

1. **Oversell:** dos personas compran la última unidad. Solución H1: la primera en confirmar pago se la lleva, la segunda recibe email "se acabó justo, te devolvemos el pago".
2. **Pago aprobado pero falla webhook:** retry automático, log para revisión manual. Cliente ve "procesando" hasta resolver.
3. **Cliente paga y cierra navegador:** confirmación por email siempre llega. El estado de la orden se ve en /cuenta/ordenes.
4. **Devolución parcial:** un cliente devuelve 1 de 3 productos. Soportar refund parcial.
5. **Dirección inválida:** validación básica en checkout (campos obligatorios + formato de teléfono).

## Checklist antes de entregar

- [ ] ¿Funciona en móvil 360px sin scroll horizontal?
- [ ] ¿Checkout en máximo 3 pasos visuales?
- [ ] ¿Guest checkout funciona?
- [ ] ¿Carrito persiste a refresh?
- [ ] ¿Hay tracking en cada paso del funnel?
- [ ] ¿Los edge cases de stock están manejados?
- [ ] ¿Hay políticas legales accesibles desde checkout?
- [ ] ¿Performance LCP < 2.5s en 4G?
