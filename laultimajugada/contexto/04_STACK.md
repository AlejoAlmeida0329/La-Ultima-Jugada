# 04_STACK — Arquitectura técnica

> Decisiones de stack, integraciones y setup del repositorio. Cargar cuando se trabaje en setup, infraestructura, integraciones o decisiones técnicas.

---

## Filosofía del stack

1. **Mínimo viable, máximo escalable.** Nada que requiera DevOps dedicado en H1.
2. **Decisiones reversibles** donde sea posible. Si algo no funciona, se cambia en < 1 semana.
3. **Optimizado para Claude Code.** Stack popular, bien documentado, con ejemplos abundantes en training data.
4. **Costo bajo en H1.** Apuntar a < $50 USD/mes en costos fijos.

---

## Arquitectura general

```
                   ┌──────────────────────┐
                   │   Vercel (Edge CDN)  │
                   │   Next.js 15 App      │
                   └──────────┬───────────┘
                              │
            ┌─────────────────┼─────────────────┐
            │                 │                 │
       ┌────▼────┐      ┌─────▼──────┐    ┌────▼─────┐
       │ Supabase │      │ Cloudinary │    │  Wompi   │
       │ (Postgres│      │  (imágenes) │    │ (pagos)  │
       │  + Auth) │      └─────────────┘    └──────────┘
       └──────────┘
            │
       ┌────▼────┐                          ┌──────────┐
       │ Resend   │◄─────────────────────── │ PostHog  │
       │ (emails) │                          │(analytics│
       └──────────┘                          └──────────┘
```

---

## Frontend

| Pieza | Decisión | Por qué |
|---|---|---|
| Framework | **Next.js 15 (App Router)** | SSR + edge, React Server Components, comunidad masiva |
| Lenguaje | **TypeScript strict** | Reducir bugs en runtime, mejor DX con Claude Code |
| Estilos | **Tailwind CSS** | Velocidad de iteración, consistencia con design tokens |
| Componentes | **shadcn/ui** | Radix bajo el capó, copy-paste no dependencia |
| Animación | **Framer Motion** | Microinteracciones de calidad sin pelear con Tailwind |
| Forms | **React Hook Form + Zod** | Validación tipada, performance |
| Iconos | **Lucide React** | Estilo consistente con shadcn |
| State del cliente | **Zustand** | Para carrito y UI state. Sin Redux. |
| Data fetching server | **Server Components + Server Actions** | Patrón estándar Next 15 |

---

## Backend / datos

| Pieza | Decisión |
|---|---|
| Base de datos | **Supabase Postgres** |
| Auth | **Supabase Auth** (email + magic link) |
| Storage de imágenes | **Cloudinary** (no Supabase Storage) |
| Lógica server-side | **Next.js API Routes + Server Actions** |
| Webhooks | **Next.js API Routes** (`/api/webhooks/wompi`) |
| Row Level Security | **Habilitada** en todas las tablas |

### Por qué Cloudinary y no Supabase Storage

- Transformaciones automáticas (WebP/AVIF, responsive)
- CDN global incluido
- 25k transformaciones/mes gratis
- Pipeline de e-commerce probado

### Por qué Supabase y no Firebase / Neon directo

- Postgres real (Firebase es NoSQL, peor para comercio)
- Auth + DB + Storage en un solo dashboard
- RLS nativo (seguridad declarativa)
- Tiers gratuitos generosos para H1

---

## Integraciones

### Wompi (pagos)

- Pasarela colombiana
- Métodos soportados: tarjeta, PSE, Nequi, Bancolombia Transfer
- Comisión: 2.65% + $700 COP por transacción exitosa
- Requiere RUT para activar cuenta
- Webhook de eventos: `transaction.updated` → marcar orden como pagada

Flujo:
1. Cliente confirma checkout
2. Frontend crea transacción en Wompi (Web Checkout)
3. Wompi redirecciona a su widget
4. Cliente paga
5. Wompi llama webhook → API Route `/api/webhooks/wompi`
6. Server actualiza estado de orden + decrementa stock + envía email de confirmación

### Cloudinary (imágenes)

- Cloud name + API key
- Folder structure: `laultimajugada/productos/[sku]/`
- Transformaciones por URL: `?w=800&q=auto&f=auto`
- Upload signed desde el admin (no API key expuesta)

### Resend (emails)

- Emails transaccionales: confirmación, envío, devolución
- Dominio propio para envío: `noreply@laultimajugada.co`
- Templates en React Email (componentes JSX)
- 3.000 emails/mes gratis

Listado mínimo de plantillas:
- `order-confirmed.tsx`
- `order-shipped.tsx`
- `order-delivered.tsx`
- `cart-abandoned.tsx` (H2)
- `restock-alert.tsx` (H2)
- `password-reset.tsx`

### PostHog (analytics)

- Product analytics + session replay + funnels
- Eventos clave a trackear:
  - `pdp_viewed`
  - `add_to_cart`
  - `checkout_started`
  - `checkout_step_completed`
  - `purchase_completed`
- Heatmaps en home y PDPs
- 1M eventos/mes gratis

### Vercel (hosting)

- Hobby tier en H1 (gratis)
- Pro tier ($20/mes) si se necesita comercial cron jobs o más bandwidth
- Preview deploys por PR (automático)
- Edge functions para webhooks

---

## Estructura del repositorio

```
/laultimajugada
├── CLAUDE.md                       ← Entry point Claude Code
├── README.md                       ← Setup técnico humano
├── package.json
├── tsconfig.json
├── next.config.ts
├── tailwind.config.ts
├── postcss.config.mjs
├── .env.example                    ← Plantilla de variables
├── .env.local                      ← NO commitear (gitignore)
│
├── /contexto                       ← Los 7 documentos
│   ├── 00_BRIEF.md
│   ├── 01_PRD.md
│   ├── 02_BRAND.md
│   ├── 03_VOICE.md
│   ├── 04_STACK.md
│   ├── 05_LEGAL.md
│   └── 06_CATALOGO.md
│
├── /skills                         ← Los 6 skills
│   ├── brand-designer.md
│   ├── copywriter.md
│   ├── ecommerce-architect.md
│   ├── product-photographer.md
│   ├── admin-ux.md
│   └── legal-disclosure.md
│
├── /docs
│   ├── /decisiones                 ← ADRs (Architecture Decision Records)
│   └── /setup                      ← Guías de setup local y deploy
│
├── /src
│   ├── /app                        ← Next App Router
│   │   ├── /(public)
│   │   │   ├── layout.tsx
│   │   │   ├── page.tsx            ← Home
│   │   │   ├── /tienda
│   │   │   │   ├── page.tsx
│   │   │   │   └── /[coleccion]/page.tsx
│   │   │   ├── /producto/[slug]/page.tsx
│   │   │   ├── /carrito/page.tsx
│   │   │   ├── /checkout/page.tsx
│   │   │   ├── /orden/[id]/page.tsx
│   │   │   ├── /cuenta/...
│   │   │   ├── /faq/page.tsx
│   │   │   ├── /devoluciones/page.tsx
│   │   │   ├── /replicas/page.tsx
│   │   │   ├── /envios/page.tsx
│   │   │   ├── /contacto/page.tsx
│   │   │   └── /sobre/page.tsx
│   │   ├── /(admin)
│   │   │   └── /admin
│   │   │       ├── layout.tsx
│   │   │       ├── page.tsx        ← Dashboard
│   │   │       ├── /catalogo
│   │   │       ├── /ordenes
│   │   │       ├── /inventario
│   │   │       ├── /clientes
│   │   │       ├── /cupones
│   │   │       └── /config
│   │   └── /api
│   │       └── /webhooks
│   │           └── /wompi/route.ts
│   │
│   ├── /components
│   │   ├── /ui                     ← shadcn primitives
│   │   ├── /marketing              ← hero, footer, nav
│   │   ├── /shop                   ← product card, gallery, etc
│   │   ├── /checkout
│   │   └── /admin
│   │
│   ├── /lib
│   │   ├── /supabase               ← client + server clients
│   │   ├── /wompi                  ← integración
│   │   ├── /cloudinary
│   │   ├── /resend                 ← templates + send
│   │   ├── /posthog
│   │   └── /utils
│   │
│   ├── /types                      ← TypeScript types compartidos
│   ├── /styles
│   │   └── globals.css
│   └── /stores                     ← Zustand stores
│
├── /supabase
│   ├── /migrations                 ← SQL migrations
│   ├── seed.sql
│   └── config.toml
│
├── /emails                         ← React Email templates
│
└── /public                         ← Static assets
```

---

## Variables de entorno

`.env.example` (plantilla en repo):

```bash
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_APP_ENV=development

# Supabase
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Wompi
NEXT_PUBLIC_WOMPI_PUBLIC_KEY=
WOMPI_PRIVATE_KEY=
WOMPI_EVENTS_SECRET=
WOMPI_INTEGRITY_SECRET=

# Cloudinary
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
CLOUDINARY_UPLOAD_PRESET=

# Resend
RESEND_API_KEY=
RESEND_FROM_EMAIL=noreply@laultimajugada.co

# PostHog
NEXT_PUBLIC_POSTHOG_KEY=
NEXT_PUBLIC_POSTHOG_HOST=https://app.posthog.com
```

**Nunca commitear `.env.local`.** Asegurar que está en `.gitignore`.

---

## CLAUDE.md — Entry point del proyecto

Este es el archivo que Claude Code lee primero cuando se abre el repo. Plantilla:

```markdown
# La Última Jugada

E-commerce de réplicas premium de camisetas de la selección Colombia.
Operado desde Bogotá. Stack Next.js + Supabase + Wompi.

## Estado actual del proyecto
[Actualizar manualmente al cierre de cada sesión grande]

## Estructura
- `/contexto` — 7 documentos que definen el proyecto. Cargar según necesidad.
- `/skills` — 6 manuales operativos. Cargar según la tarea.
- `/src` — código de la aplicación.
- `/supabase` — schema y migraciones.

## Patrones típicos de carga de contexto

Al iniciar sesión nueva en Claude Code, según el tipo de tarea:

**Diseñar nueva pantalla pública:**
- Cargar `contexto/01_PRD.md`, `contexto/02_BRAND.md`, `contexto/03_VOICE.md`
- Cargar `skills/brand-designer.md`, `skills/copywriter.md`, `skills/ecommerce-architect.md`, `skills/legal-disclosure.md`

**Trabajar en admin:**
- Cargar `contexto/01_PRD.md`, `contexto/06_CATALOGO.md`
- Cargar `skills/brand-designer.md`, `skills/admin-ux.md`

**Integrar nuevo servicio (Wompi, Cloudinary, etc):**
- Cargar `contexto/04_STACK.md`
- Documentar la decisión en `/docs/decisiones/`

**Escribir copy para nueva página:**
- Cargar `contexto/03_VOICE.md`, `contexto/05_LEGAL.md`
- Cargar `skills/copywriter.md`, `skills/legal-disclosure.md`

**Auditar antes de publicar:**
- Cargar `contexto/05_LEGAL.md`
- Cargar `skills/legal-disclosure.md`

## Comandos comunes

```bash
npm run dev              # Desarrollo local
npm run build            # Build de producción
npm run lint             # ESLint
npm run typecheck        # tsc --noEmit
supabase start           # DB local
supabase db reset        # Reset + seed
supabase db push         # Aplicar migraciones a remoto
```

## Reglas duras del proyecto

1. Nunca commitear `.env.local`.
2. Nunca usar marcas registradas en código, naming, meta tags o copy (ver `legal-disclosure`).
3. Todo cambio que afecte la base de datos va con migración SQL versionada.
4. Toda decisión arquitectónica importante va documentada en `/docs/decisiones/`.
5. Antes de cada deploy a producción: `npm run lint && npm run typecheck && npm test`.

## Contactos clave
- Abogado: [pendiente]
- Contador: [pendiente]
- Proveedor producto: [pendiente]
- Transportadora: [pendiente]
```

---

## Roadmap técnico H1 (8 semanas)

### Semanas 1–2: Setup base
- Inicializar repo + Next.js + TypeScript + Tailwind + shadcn
- Configurar Supabase (DB + Auth)
- Crear schema según `06_CATALOGO.md`
- Configurar Vercel + dominio
- Layouts públicos + admin básicos
- Sistema de diseño base con design tokens del `02_BRAND.md`

### Semanas 3–4: Catálogo y PDP
- Lista de productos con filtros
- Páginas de colección
- Product Detail Page (PDP) completa
- Integración Cloudinary
- Galería con carrusel mobile
- SEO básico (meta tags, sitemap, schema)

### Semanas 5–6: Carrito y checkout
- Carrito persistente con Zustand + Supabase
- Checkout en 1 página, 3 pasos
- Integración Wompi (Web Checkout)
- Webhook + actualización de orden
- Decremento de stock al pagar
- Email de confirmación con Resend

### Semanas 7–8: Admin
- Login admin (Supabase Auth)
- Dashboard básico
- CRUD productos + variantes
- Upload de imágenes con Cloudinary
- Gestión de órdenes (lista + detalle + cambio de estado)
- Vista de inventario
- Páginas legales editables

### Hito de cierre H1
- 10–15 SKUs publicados
- Primera orden real procesada de extremo a extremo
- Todos los emails transaccionales funcionando
- PostHog con eventos clave instrumentados
- Documentos legales publicados y revisados por abogado

---

## Costos estimados mensuales

### Fijos H1 (escala baja)

| Servicio | Costo mes |
|---|---|
| Vercel Hobby | $0 |
| Supabase Free | $0 |
| Cloudinary Free | $0 |
| Resend Free | $0 |
| PostHog Free | $0 |
| Dominio (.co) | ~$2.50 USD |
| **Total fijo** | **~$3 USD/mes** |

### Variables

| Servicio | Variable |
|---|---|
| Wompi | 2.65% + $700 COP por transacción exitosa |

### Proyección a mes 6 (600 órdenes / AOV $130k)

| Concepto | Monto mes 6 |
|---|---|
| GMV | $78M COP |
| Wompi fee (~3%) | ~$2.5M COP |
| Vercel Pro (probable) | $80k COP |
| Supabase Pro (probable) | $100k COP |
| Logística variable | depende de transportadora |

---

## Decisiones diferidas (no son H1)

Documentadas para no olvidar:

| Decisión | Cuándo evaluar |
|---|---|
| Cambiar Vercel Hobby → Pro | Cuando se necesite cron jobs comerciales o > 100 GB bandwidth |
| Migrar Supabase Free → Pro | Cuando se acerque al límite de 500 MB DB |
| Integrar facturación electrónica | Cuando se constituya SAS |
| Agregar Mercado Pago como fallback | Si Wompi tiene downtime recurrente |
| Personalización de camisetas (nombre + número) | H2, requiere flujo de proveedor distinto |
| App móvil nativa | Solo si la web no resuelve, probable H4+ |
| Reservas temporales de stock en checkout | H3, cuando volumen sea > 50 órdenes/día |

---

## Checklist técnico pre-lanzamiento

- [ ] Repo en GitHub con `.gitignore` correcto
- [ ] Deploy en Vercel funcionando
- [ ] Dominio apuntando a Vercel con SSL
- [ ] Supabase migrations aplicadas en producción
- [ ] RLS habilitado en todas las tablas
- [ ] Wompi en modo producción + webhook verificado
- [ ] Cloudinary configurado con upload preset
- [ ] Resend con dominio propio verificado (`laultimajugada.co`)
- [ ] PostHog instalado con eventos clave instrumentados
- [ ] PostHog session replay activado
- [ ] PageSpeed Insights > 85 en móvil
- [ ] LCP < 2.5s en 4G
- [ ] `robots.txt` y `sitemap.xml` correctos
- [ ] Schema.org Product en PDPs
- [ ] Las 7 páginas legales publicadas
- [ ] 10–15 SKUs con fotos completas según `product-photographer` skill
- [ ] Primera orden de prueba completada de extremo a extremo
- [ ] Backup automático de Supabase configurado
