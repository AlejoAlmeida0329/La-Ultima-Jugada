# La Última Jugada

E-commerce de réplicas premium de camisetas de la selección Colombia.
Operado desde Bogotá. Stack Next.js + Supabase + Wompi.

---

## Estado actual del proyecto

**Fase:** Setup inicial — repositorio de contexto creado, código aún no inicializado.

**Próximos hitos:**
- Inicialización del proyecto Next.js
- Setup de Supabase
- Implementación del schema de catálogo

> Actualizar esta sección al cierre de cada sesión grande de trabajo.

---

## Estructura del repositorio

```
/laultimajugada
├── CLAUDE.md                    ← Este archivo. Entry point.
├── README.md                    ← Setup técnico para desarrolladores
├── /contexto                    ← 7 documentos que definen el proyecto
├── /skills                      ← 6 manuales operativos por dominio
├── /src                         ← (Próximamente) código de la aplicación
└── /supabase                    ← (Próximamente) schema y migraciones
```

---

## Documentos de contexto (carpeta `/contexto`)

Cargar según necesidad. No es necesario cargar todos en cada sesión.

- `00_BRIEF.md` — Visión, audiencia, propuesta de valor, roadmap
- `01_PRD.md` — Requerimientos del producto, sitemap, user stories
- `02_BRAND.md` — Identidad visual: paleta, tipografía, sistema gráfico
- `03_VOICE.md` — Tono, voz, microcopy, ejemplos do/don't
- `04_STACK.md` — Arquitectura técnica, integraciones, roadmap H1
- `05_LEGAL.md` — Política de réplicas, devoluciones, marco fiscal
- `06_CATALOGO.md` — Modelo de datos del catálogo, SKUs, variantes

## Skills (carpeta `/skills`)

Manuales operativos por dominio. Cargar según la tarea, no como conjunto.

- `brand-designer.md` — Aplicación de la marca en UI y piezas
- `copywriter.md` — Cómo escribir en voz LUJ
- `ecommerce-architect.md` — Flujos y lógica de comercio
- `product-photographer.md` — Brief y guidelines de fotografía
- `admin-ux.md` — Patrones para un admin usable por no técnicos
- `legal-disclosure.md` — Filtro legal operativo del día a día

---

## Patrones de carga de contexto

Al iniciar una sesión nueva en Claude Code, según el tipo de tarea cargá los archivos necesarios:

### Diseñar nueva pantalla pública
- `contexto/01_PRD.md`, `contexto/02_BRAND.md`, `contexto/03_VOICE.md`
- `skills/brand-designer.md`, `skills/copywriter.md`, `skills/ecommerce-architect.md`, `skills/legal-disclosure.md`

### Trabajar en el admin
- `contexto/01_PRD.md`, `contexto/06_CATALOGO.md`
- `skills/brand-designer.md`, `skills/admin-ux.md`

### Integrar nuevo servicio (Wompi, Cloudinary, etc.)
- `contexto/04_STACK.md`
- Documentar la decisión en `/docs/decisiones/`

### Escribir copy para nueva página
- `contexto/03_VOICE.md`, `contexto/05_LEGAL.md`
- `skills/copywriter.md`, `skills/legal-disclosure.md`

### Auditar antes de publicar al público
- `contexto/05_LEGAL.md`
- `skills/legal-disclosure.md`

### Sesión de fotos / catálogo nuevo
- `contexto/02_BRAND.md`, `contexto/06_CATALOGO.md`
- `skills/product-photographer.md`

---

## Comandos comunes (cuando el código exista)

```bash
npm run dev              # Servidor de desarrollo local
npm run build            # Build de producción
npm run lint             # ESLint
npm run typecheck        # TypeScript check sin emit
supabase start           # Base de datos local
supabase db reset        # Reset + seed
supabase db push         # Aplicar migraciones a remoto
```

---

## Reglas duras del proyecto

1. **Nunca commitear `.env.local`** ni ningún archivo con credenciales.
2. **Nunca usar marcas registradas** en código, naming, meta tags o copy. Ver `skills/legal-disclosure.md`.
3. **Todo cambio que afecte la base de datos** va con migración SQL versionada en `/supabase/migrations`.
4. **Toda decisión arquitectónica importante** va documentada como ADR en `/docs/decisiones/`.
5. **Antes de cada deploy a producción:** `npm run lint && npm run typecheck`.
6. **Naming de producto siempre genérico.** Sin "Adidas", "oficial", "FCF", "auténtico". Ver `legal-disclosure`.

---

## Contactos clave

> Actualizar cuando se vayan estableciendo.

- **Operador:** Alejandro
- **Abogado:** _pendiente_
- **Contador:** _pendiente_
- **Proveedor producto:** _pendiente_
- **Transportadora:** _pendiente_
- **Fotógrafo freelance:** _pendiente_

---

## Información fiscal

Operación inicial como **persona natural comerciante** (RUT requerido para Wompi).
Constitución de SAS evaluada cuando ingresos mensuales > $20M COP sostenidos.
Detalle completo en `contexto/05_LEGAL.md`.
