# 00_BRIEF — La Última Jugada

> Documento maestro de contexto. Resume el proyecto en una pasada.
> Cargar siempre que se inicie una sesión nueva en Claude Code.

---

## Marca

**La Última Jugada**

La jugada que define el partido. La última repetición que cuenta. El último kilómetro antes de la meta.

Un nombre, tres territorios deportivos.

---

## Visión

Convertir a La Última Jugada en la tienda de referencia en Colombia para ropa deportiva con actitud — partiendo de camisetas de selección, expandiendo a entrenamiento y running.

## Misión

Vestir al hincha y al atleta con prendas de calidad premium, sin el sobreprecio de las marcas globales y sin la experiencia de mierda de comprar por WhatsApp.

---

## Producto

- **Mes 0–6:** réplicas premium 1:1 de camisetas de la Selección Colombia. Local, visitante, retro, ediciones especiales (tipo Macondo, Centenario).
- **Mes 6+:** expansión a gym y running. Producto curado primero, marca propia después.

Pricing: variable por producto, gestionable desde admin. Sin precio fijo.

---

## Audiencia

**Núcleo:** hombres y mujeres 18–35, hinchas, deportistas casuales, conocedores de fútbol.

**Secundario:** papás comprando para hijos, regalos para parejas y familiares.

**Geografía:** Colombia nacional. Foco inicial Bogotá, Medellín, Cali, Barranquilla.

---

## Propuesta de valor

1. **Calidad real 1:1** — la diferencia clara con la merca de San Andresito.
2. **Catálogo curado** — no somos bodega, somos selección.
3. **Experiencia digital decente** — comprás como en cualquier tienda seria, no negociás por WhatsApp.
4. **Envío nacional confiable** — tracking, soporte, devoluciones claras.
5. **Marca con identidad propia** — no somos un revendedor anónimo.

---

## Posicionamiento

| Por encima de | Diferenciado por | Por debajo de |
|---|---|---|
| Vendedores WhatsApp / Marketplace | Marca, curaduría, experiencia digital | Tienda oficial Adidas / FCF |
| San Andresito | Calidad declarada y consistente | (en precio, no en calidad de venta) |
| Dropshipping chino directo | Stock local, envío rápido, soporte | |

---

## Política de réplicas — innegociable

- Transparencia total: **"réplica premium calidad 1:1"**.
- Nunca usar "original" ni "oficial" en producto o copy.
- Naming genérico: *"Camiseta Selección Colombia – Local 25/26"*, no *"Camiseta Adidas Colombia"*.
- Sin marcas registradas en dominio, meta tags, ni keywords pagas.
- Política de réplicas visible en footer y FAQ.
- Política de devoluciones clara.

Detalle completo en `05_LEGAL.md`.

---

## Modelo de negocio

- E-commerce directo (D2C).
- Pricing por producto, margen por validar referencia a referencia.
- Sin tiendas físicas en horizonte cercano.
- Pagos: Wompi (tarjeta, PSE, Nequi, Bancolombia transfer).
- Operación inicial como persona natural comerciante (sin SAS constituida).

---

## Métricas norte

| Métrica | Objetivo mes 6 |
|---|---|
| Envíos nacionales / mes | 600 |
| Conversion rate | 2–3% |
| AOV | $110–140k COP |
| Repeat purchase 90 días | 15% |
| NPS | 60+ |

---

## Roadmap por horizontes

**H1 — Mes 1–2: MVP**
- Sitio público + admin custom
- Catálogo selección Colombia: 10–15 SKUs iniciales
- Checkout funcional con Wompi
- Logística con una transportadora nacional
- Política legal y de devoluciones publicada

**H2 — Mes 3–4: Catálogo y profundidad**
- Catálogo completo de selección (local, visitante, alternativas, retro)
- Ediciones especiales
- Variantes hombre / mujer / niño cuando aplique
- Programa de referidos básico

**H3 — Mes 5–6: Optimización y escala**
- Optimización de funnel basada en datos PostHog
- Primera campaña paga (Meta + Google)
- Email marketing automatizado (carrito abandonado, post-compra, retorno)
- Fidelización: descuento segunda compra

**H4 — Mes 7–12: Expansión vertical**
- Línea de ropa de gimnasio (curada o marca propia)
- Línea de running
- Posible marca propia en silueta deportiva básica
- Evaluar segundo país (México probable, siguiendo rails Tikin)

---

## Stack técnico (resumen)

Detalle completo en `04_STACK.md`.

- **Frontend:** Next.js 15 (App Router) + TypeScript + Tailwind + shadcn/ui
- **Backend:** Supabase (Postgres + Auth + Storage + RLS)
- **Admin:** custom con shadcn — pensado para uso no técnico
- **Pagos:** Wompi (tarjeta, PSE, Nequi, Bancolombia)
- **Imágenes:** Cloudinary
- **Email:** Resend
- **Analytics:** PostHog
- **Hosting:** Vercel
- **Método de desarrollo:** Claude Code con SuperClaude

---

## Riesgos conocidos

1. **Legal:** venta de réplicas online es más visible que por WhatsApp. Mitigación con política de réplicas y naming genérico, pero el riesgo no es cero.
2. **Operativo:** sin proveedor fijo, calidad puede variar. Definir QC mínimo por lote antes de publicar.
3. **Stock:** sin sistema de inventario robusto en H1, riesgo de oversell. Empezar con publicación manual de disponibilidad.
4. **Logística:** un solo transportador es un punto único de falla. Negociar segundo proveedor antes de mes 3.

---

## Equipo y operación

- **Alejandro:** dirección, producto, decisiones de catálogo y marca
- **Por contratar (mes 3–4):** persona de operación logística + soporte al cliente
- **Externo:** fotógrafo de producto (freelance por sesión)
