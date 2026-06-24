# La Última Jugada

E-commerce de réplicas premium de camisetas de la selección Colombia.

## Stack

- **Frontend:** Next.js 15 + TypeScript + Tailwind + shadcn/ui
- **Backend:** Supabase (Postgres + Auth)
- **Pagos:** Wompi
- **Imágenes:** Cloudinary
- **Email:** Resend
- **Analytics:** PostHog
- **Hosting:** Vercel

## Documentación

Toda la documentación del proyecto está en:

- `/contexto` — 7 documentos: brief, PRD, brand, voice, stack, legal, catálogo
- `/skills` — 6 manuales operativos por dominio
- `CLAUDE.md` — Entry point para Claude Code

Empezar leyendo `CLAUDE.md`.

## Setup local

> Pendiente de inicialización del código.

```bash
# Instalar dependencias
npm install

# Variables de entorno
cp .env.example .env.local
# Editar .env.local con tus credenciales

# Base de datos local
supabase start

# Servidor de desarrollo
npm run dev
```

## Estructura

```
laultimajugada/
├── CLAUDE.md                    ← Entry point Claude Code
├── README.md                    ← Este archivo
├── .gitignore
├── /contexto                    ← Documentos del proyecto
├── /skills                      ← Manuales operativos
├── /src                         ← (Próximamente) código
└── /supabase                    ← (Próximamente) schema
```

## Licencia

Privado. Todos los derechos reservados.
