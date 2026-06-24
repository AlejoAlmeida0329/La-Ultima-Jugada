# 01_PRD — La Última Jugada

> Requerimientos del producto digital. Cargar cuando se trabaje en features, user stories, UI o flujos.

---

## Objetivos del producto

1. Vender en línea de forma confiable, sin pasar por WhatsApp.
2. Permitir gestión de catálogo por una persona no técnica.
3. Convertir tráfico a venta con un funnel limpio (mobile-first).
4. Construir base de clientes con datos propios (no atrapados en plataformas).

---

## Stakeholders

| Rol | Persona |
|---|---|
| Producto / dirección | Alejandro |
| Operación catálogo | Alejandro (H1) → persona delegada (H2+) |
| Soporte cliente | Alejandro (H1) → persona delegada (H2+) |
| Logística | Tercerizada (transportadora nacional) |

---

## Personas

### Daniel — 27, hincha, comprador principal
- Compra por WhatsApp porque no hay alternativa decente
- Le da pereza negociar precio y esperar respuesta
- Quiere ver fotos reales del producto, no renders
- Compra desde el celular en 90% de los casos
- Le importa que llegue rápido y que sea calidad real

### María — 45, mamá compradora de regalo
- Compra la camiseta para el hijo de 15
- No conoce de fútbol técnico, pero conoce la selección
- Necesita guía de tallas clara
- Paga con tarjeta, no transferencia
- Necesita factura

### Catalina — Admin del catálogo
- No es técnica
- Necesita subir un producto en menos de 5 minutos
- Necesita poder duplicar productos (variantes de un mismo modelo)
- Necesita ver claramente qué está publicado y qué no
- No quiere romper nada por accidente

---

## Sitemap público

```
/
├── /                          ← Home
├── /tienda                    ← Catálogo con filtros
├── /tienda/[coleccion]        ← Catálogo por colección
├── /producto/[slug]           ← Product Detail Page (PDP)
├── /carrito                   ← Carrito
├── /checkout                  ← Checkout (1 página, 3 pasos visuales)
├── /orden/[id]                ← Confirmación
├── /cuenta                    ← Mi cuenta
│   ├── /cuenta/ordenes
│   ├── /cuenta/datos
│   └── /cuenta/direcciones
├── /faq                       ← Preguntas frecuentes
├── /devoluciones              ← Política de devoluciones
├── /replicas                  ← Política de réplicas
├── /envios                    ← Política de envíos
├── /contacto                  ← Contacto / soporte
└── /sobre                     ← Sobre la marca
```

---

## Sitemap admin

```
/admin
├── /admin/login
├── /admin                     ← Dashboard
├── /admin/catalogo
│   ├── /admin/catalogo/productos
│   ├── /admin/catalogo/productos/nuevo
│   ├── /admin/catalogo/productos/[id]
│   ├── /admin/catalogo/colecciones
│   └── /admin/catalogo/categorias
├── /admin/inventario          ← Stock por variante
├── /admin/ordenes
│   ├── /admin/ordenes
│   └── /admin/ordenes/[id]
├── /admin/clientes
├── /admin/cupones
└── /admin/config              ← Envío, pagos, info tienda
```

---

## User stories — clientes

### Navegación y descubrimiento
- Como cliente, quiero ver el catálogo filtrable por género, colección y talla, para encontrar rápido lo que busco.
- Como cliente, quiero ver fotos de alta resolución desde múltiples ángulos antes de comprar.
- Como cliente, quiero ver una guía de tallas con medidas reales (cm).
- Como cliente, quiero ver si el producto está disponible en mi talla antes de meter al carrito.

### Compra
- Como cliente, quiero comprar sin crear cuenta (guest checkout).
- Como cliente, quiero pagar con tarjeta, PSE o Tikin.
- Como cliente, quiero ver claramente el costo de envío ($12.000) antes de confirmar.
- Como cliente, quiero recibir confirmación por correo inmediatamente.
- Como cliente, quiero un número de orden para hacer seguimiento.

### Post-compra
- Como cliente, quiero saber cuándo llega mi pedido (estado de orden).
- Como cliente, quiero poder solicitar devolución desde mi cuenta.
- Como cliente, quiero recibir el tracking de envío por correo.

### Confianza
- Como cliente, quiero ver claramente que son réplicas premium (no me quiero engañar).
- Como cliente, quiero leer política de devoluciones antes de comprar.
- Como cliente, quiero ver el contacto de soporte fácilmente.

---

## User stories — admin

### Catálogo
- Como admin, quiero crear un producto con sus variantes en menos de 5 minutos.
- Como admin, quiero duplicar un producto existente para no rehacer todo.
- Como admin, quiero subir fotos arrastrando y soltando, con reorden.
- Como admin, quiero ver el preview de cómo se verá el producto en la tienda antes de publicar.
- Como admin, quiero marcar productos como destacados (featured).
- Como admin, quiero archivar productos sin eliminarlos.

### Inventario
- Como admin, quiero ver el stock de cada variante en una tabla.
- Como admin, quiero ajustar stock de varias variantes a la vez (bulk edit).
- Como admin, quiero ver alertas cuando una variante está por debajo de un umbral.

### Órdenes
- Como admin, quiero ver órdenes filtradas por estado.
- Como admin, quiero cambiar el estado de una orden (pagada, despachada, entregada, devuelta).
- Como admin, quiero agregar notas internas a una orden.
- Como admin, quiero imprimir o exportar guías para la transportadora.

### Configuración
- Como admin, quiero editar las políticas (devoluciones, réplicas, envíos) desde el admin.
- Como admin, quiero crear cupones de descuento con código.
- Como admin, quiero ver métricas básicas en el dashboard (ventas día/semana/mes, AOV, conversión).

---

## Criterios de aceptación duros

| Criterio | Objetivo |
|---|---|
| Performance LCP móvil 4G | < 2.5s |
| Mobile-first | 100% del flujo funciona en 360px de ancho |
| Checkout | Máximo 3 pasos visuales en una página |
| Imágenes | Lazy load + WebP/AVIF servidas por Cloudinary |
| SEO básico | sitemap.xml, robots.txt, meta tags por producto |
| Accesibilidad | WCAG AA en color contrast, navegación por teclado |
| Política de réplicas | Visible desde footer, link en PDP |
| Carrito persistente | Sobrevive a refresh y entre sesiones (localStorage + DB si logueado) |

---

## Reglas de negocio

1. **Envío:** flat $12.000 COP a todo el país en H1.
2. **Pagos:** tarjeta, PSE y Tikin Checkout. Sin contra-entrega.
3. **Devoluciones:** 8 días calendario desde recibido. Producto sin uso, etiquetas puestas.
4. **Cambios:** permitidos por talla en mismo modelo, cliente paga envío.
5. **Sin stock:** producto visible pero CTA cambia a "Notifícame cuando llegue".
6. **Naming de producto:** siempre genérico, nunca con marca registrada (ver `05_LEGAL.md`).

---

## Out of scope para H1

Para no perder foco:

- Multi-idioma
- Multi-moneda
- Programa de afiliados / referidos
- Reviews de producto
- Wishlist
- Live chat
- Suscripciones
- App móvil nativa
- Compra por WhatsApp integrada
- Personalización (nombre, número en camiseta)
- Multi-bodega

A evaluar en H2+ según data.

---

## Notas de futuro (no construir en H1)

- **Envío por zonas:** evaluar pasar de flat a 2–3 zonas con base en data real de costos.
- **Free shipping sobre $X:** evaluar como anchor para subir AOV.
- **Personalización con nombre y número:** alta demanda esperada en camisetas. Requiere flujo de proveedor distinto.
- **Reviews:** evaluar con plataforma tipo Junip o Stamped en H2.

---

## Riesgos del producto digital

1. **Oversell:** sin stock en tiempo real, riesgo de vender lo que no hay. Mitigación: stock manual + alertas + bloqueo automático en 0.
2. **Fraude de pago:** evaluar reglas anti-fraude del gateway. Sin contra-entrega reduce mucho el riesgo.
3. **Abandono de carrito:** esperado en e-commerce. Mitigación: email automatizado a las 2h con recordatorio.
4. **Devoluciones por talla:** alto en ropa. Mitigación: guía de tallas con medidas reales + tabla por modelo.
