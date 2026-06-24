# 06_CATALOGO — Estructura del catálogo

> Modelo de datos del catálogo de producto. Cargar cuando se trabaje en base de datos, admin, API o flows de catálogo.

---

## Filosofía de modelado

Camiseta de hombre y camiseta de mujer son **productos separados**, no variantes de uno solo. Razones:

- Fotografía distinta (modelo, fit, ángulos)
- Tallas siguen estándares distintos (M de hombre ≠ M de mujer)
- SEO independiente
- Stock se gestiona por separado

Se relacionan vía `collection` y vía `related_products`.

**Pricing es único por producto.** Todas las tallas de un producto cuestan lo mismo. Las variantes solo manejan talla y stock.

---

## Entidades principales

### `products`

Producto vendible. Una unidad comercial con sus variantes de talla.

```
id                  uuid PK
slug                text unique         "tricolor-25-26-local-hombre"
name                text                "Tricolor 25/26"
subtitle            text                "Local Hombre"
collection_id       uuid FK
description         text (rich)         descripción larga, markdown sanitizado
short_description   text                1 línea para cards
price               integer (COP)       precio en pesos enteros, sin decimales
compare_at_price    integer (COP)       opcional, para precio tachado
status              enum                draft | active | archived
featured            boolean             aparece en home
sort_order          integer             orden manual en colecciones
meta_title          text                SEO
meta_description    text                SEO
created_at          timestamptz
updated_at          timestamptz
```

### `product_variants`

Cada talla disponible de un producto. Una variante = una SKU comprable.

```
id              uuid PK
product_id      uuid FK
sku             text unique         "LUJ-TRI2526-LOCALH-L"
size            enum                XS | S | M | L | XL | XXL
stock_quantity  integer             entero >= 0
weight_grams    integer             para logística futura
active          boolean             si está desactivado, no se compra
created_at      timestamptz
updated_at      timestamptz
```

### `collections`

Agrupación editorial de productos (tipo "Tricolor 25/26", "Macondo", "Centenario").

```
id              uuid PK
slug            text unique         "tricolor-25-26"
name            text                "Tricolor 25/26"
description     text
hero_image_url  text                Cloudinary URL
featured        boolean             aparece en home
sort_order      integer
status          enum                draft | active | archived
created_at      timestamptz
updated_at      timestamptz
```

### `product_media`

Imágenes y futuros videos asociados a un producto.

```
id              uuid PK
product_id      uuid FK
url             text                Cloudinary URL (transformaciones por query)
alt_text        text
media_type      enum                gallery | hero | detail | lifestyle
sort_order      integer
created_at      timestamptz
```

### `categories` (tags)

Categorías transversales que cruzan colecciones. Many-to-many con products.

```
id              uuid PK
slug            text unique
name            text
parent_id       uuid FK (nullable)  para jerarquía
```

Categorías iniciales:
- `seleccion-colombia`
- `seleccion-masculina`
- `seleccion-femenina`
- `retro`
- `edicion-especial`
- `kit-local`
- `kit-visitante`
- `kit-alternativo`

A futuro:
- `gym`
- `running`
- `accesorios`

### `product_categories` (join)

```
product_id      uuid FK
category_id     uuid FK
PK (product_id, category_id)
```

### `product_attributes`

Atributos específicos del producto para filtrado y SEO. Modelado como key-value para flexibilidad.

```
id              uuid PK
product_id      uuid FK
key             text                "team", "season", "kit_type", "year"
value           text                "seleccion-colombia", "25/26", "local", "1990"
```

Atributos canónicos para selección:
- `team`: seleccion-colombia
- `season`: 25/26, 24/25, retro
- `kit_type`: local, visitante, alternativo, portero, especial
- `year`: numérico (solo para retro)
- `gender`: hombre, mujer, nino

---

## Convención de SKU

Formato: **`LUJ-[COLECCION]-[KIT][GENDER]-[SIZE]`**

| Segmento | Ejemplo | Notas |
|---|---|---|
| `LUJ` | Fijo | Prefijo de marca |
| `COLECCION` | `TRI2526`, `MACONDO`, `CEN100` | Código corto de colección |
| `KIT` | `LOCAL`, `VISIT`, `ALTRN` | Tipo de kit |
| `GENDER` | `H`, `M`, `N` | Hombre, Mujer, Niño |
| `SIZE` | `XS`, `S`, `M`, `L`, `XL`, `XXL` | Talla |

Ejemplos:
- `LUJ-TRI2526-LOCALH-L` — Tricolor 25/26 Local Hombre talla L
- `LUJ-MACONDO-ESPM-S` — Macondo Edición Especial Mujer talla S
- `LUJ-CEN100-LOCALH-XL` — Centenario Local Hombre talla XL

El SKU se autogenera al crear el producto, pero el admin puede editarlo si necesita.

---

## Estados del ciclo de producto

```
draft ─────► active ─────► archived
                ▲                │
                └────────────────┘
```

- **draft:** no visible públicamente, en preparación
- **active:** visible y comprable (si tiene stock > 0)
- **archived:** no visible públicamente, mantiene historial de órdenes

**Importante:** no se permite eliminar productos en hard delete. Solo archivar. Esto preserva la integridad histórica de órdenes.

---

## Lógica de disponibilidad

Para un producto en frontend:

```
estado_visible = active
disponibilidad_de_compra =
  active
  AND al menos una variante con active=true AND stock_quantity > 0
```

Cuando todas las variantes están en 0:
- Producto sigue visible
- CTA cambia de "Agregar al carrito" a "Notifícame cuando llegue"
- Captura email para alerta de restock

---

## Reglas de pricing

- Precio único por producto. Todas las tallas cuestan lo mismo.
- Precio se guarda en **enteros, en pesos colombianos**, sin decimales (`120000` = $120.000).
- `compare_at_price` opcional, mayor que `price` si existe, para mostrar tachado.
- Cupones aplican a nivel de carrito, no de producto.

---

## Naming convention en UI

| Campo | Ejemplo | Donde se muestra |
|---|---|---|
| `name` | "Tricolor 25/26" | Card grande, hero |
| `subtitle` | "Local Hombre" | Bajo el name |
| `collection.name` | "Tricolor 25/26" | Breadcrumb, página de colección |
| `slug` | `tricolor-25-26-local-hombre` | URL |

URL pattern: `/producto/[slug]`

---

## Imágenes — convención de orden y tipos

Por producto, recomendado mínimo:

1. **hero** (1): foto principal frente, fondo neutro
2. **gallery** (3–5): frente, espalda, costado, en modelo, contexto
3. **detail** (2–4): escudo, logo, etiqueta, textura tela
4. **lifestyle** (0–2, opcional): foto en uso real

Total recomendado por SKU principal: **6–10 imágenes**.

Todas se sirven desde Cloudinary con transformaciones automáticas (WebP/AVIF, responsive sizes).

---

## Política de stock — H1

- Stock manual desde admin.
- Sin sincronización con sistemas externos.
- Cuando una variante llega a 0, se mantiene visible pero bloqueada para compra.
- Admin recibe alerta por correo cuando una variante baja de 3 unidades.
- Decremento de stock se hace **al confirmar la orden pagada**, no al meter al carrito (evita bloqueos por carritos abandonados).
- Riesgo aceptado: dos personas pueden comprar la última unidad simultáneamente. Volumen bajo en H1 lo hace manejable. A evaluar reserva temporal de 15 min al iniciar checkout en H3.

---

## Datos seed para arrancar

Colecciones iniciales:
- `tricolor-25-26` — Selección Colombia local/visitante actual
- `macondo` — Edición especial El Legado de Gabo
- `centenario` — 100 años Federación
- `cafetero-retro` — Camisetas retro icónicas

Categorías iniciales: ver arriba en `categories`.

10–15 SKUs iniciales como objetivo de catálogo en lanzamiento.

---

## Ejemplo concreto — Producto poblado

```yaml
product:
  slug: tricolor-25-26-local-hombre
  name: Tricolor 25/26
  subtitle: Local Hombre
  collection: tricolor-25-26
  status: active
  featured: true
  price: 130000
  compare_at_price: 180000
  description: |
    Camiseta réplica premium calidad 1:1 estilo selección Colombia,
    versión local temporada 25/26. Tela poliéster reciclado,
    tecnología transpirable, escudo bordado.
  short_description: Réplica premium calidad 1:1. Local 25/26.
  attributes:
    team: seleccion-colombia
    season: 25/26
    kit_type: local
    gender: hombre
  categories:
    - seleccion-colombia
    - seleccion-masculina
    - kit-local
  variants:
    - sku: LUJ-TRI2526-LOCALH-S
      size: S
      stock: 5
    - sku: LUJ-TRI2526-LOCALH-M
      size: M
      stock: 8
    - sku: LUJ-TRI2526-LOCALH-L
      size: L
      stock: 12
    - sku: LUJ-TRI2526-LOCALH-XL
      size: XL
      stock: 6
    - sku: LUJ-TRI2526-LOCALH-XXL
      size: XXL
      stock: 3
  media:
    - hero: foto frente fondo tiza
    - gallery: espalda, costado, en modelo
    - detail: escudo bordado, logo, etiqueta
```
