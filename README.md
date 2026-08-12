# TrainLink

Marketplace de entrenamiento personal que conecta clientes y entrenadores en España (EUR / Europe/Madrid), preparado para expansión multi-país.

> **MVP en construcción activa.** Idioma UI inicial: español. Segundo idioma preparado: inglés.

## Stack

| Capa | Tecnología |
|------|------------|
| Monorepo | pnpm 10 + Turborepo 2 + TypeScript estricto |
| API | NestJS 11, Prisma 6.19, PostgreSQL 16, Redis, BullMQ-ready |
| Web / Admin | Next.js 15.5 App Router, Tailwind, Framer Motion |
| Móvil | Expo + Expo Router |
| Pagos | Stripe Connect Express (+ proveedor simulado local/CI) |
| Archivos | MinIO (S3) |
| Email local | Mailpit |

## Requisitos

- Node.js ≥ 22
- pnpm ≥ 10
- Docker Desktop / Engine

## Arranque rápido

```bash
cp .env.example .env
docker compose up -d
pnpm install
pnpm db:generate
pnpm db:migrate
pnpm db:seed
pnpm dev
```

Script automatizado:

```bash
chmod +x infrastructure/scripts/dev-setup.sh
./infrastructure/scripts/dev-setup.sh
```

### URLs locales

| App | URL |
|-----|-----|
| Web | http://localhost:3000 |
| Admin | http://localhost:3001 |
| API / Swagger | http://localhost:4000/docs |
| Mailpit | http://localhost:8025 |
| MinIO | http://localhost:9001 |

## Credenciales DEMO (solo local)

**Contraseña de todos los usuarios demo:** `TrainLink!Dev2026`

Ejemplos (ver seed para la lista completa):

- `superadmin@demo.trainlink.local` — SUPER_ADMIN
- `admin@demo.trainlink.local` — ADMIN
- `client1@demo.trainlink.local` — CLIENT
- `trainer.madrid@demo.trainlink.local` — TRAINER

⚠️ **Nunca uses estas credenciales ni este password en staging/producción.** Desactiva el seed (`SEED_DEMO_DATA=false`).

## Scripts útiles

```bash
pnpm lint
pnpm typecheck
pnpm test
pnpm test:integration
pnpm test:e2e
pnpm build
pnpm docker:up
pnpm db:studio
```

## Documentación

- [Arquitectura](documentation/architecture.md)
- [Supuestos](documentation/assumptions.md)
- [Estado de implementación](documentation/implementation-status.md)
- [Seguridad](documentation/security.md)
- [Testing](documentation/testing.md)
- [Despliegue](documentation/deployment.md)
- [Pendientes de producción](documentation/pending-production-requirements.md)
- [Changelog de archivos](documentation/file-changelog.md)

## Estructura

```text
apps/web | admin | mobile | api
packages/ui | api-client | auth | config | constants | types | validation
infrastructure/ docker scripts nginx backups
documentation/
```

## Pagos

Sin claves Stripe, `PAYMENT_PROVIDER=simulated` permite checkout y webhooks simulados. Con claves test de Stripe se usa Connect Express (destination charges + application fee). **No es un escrow.**

## Legal

Los textos legales de la app son **BORRADOR PENDIENTE DE REVISIÓN POR UN PROFESIONAL JURÍDICO**.
