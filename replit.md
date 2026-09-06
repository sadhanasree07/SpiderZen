# SpiderZen

SpiderZen is a mobile-first industrial safety prototype for colorimetric H₂S exposure estimation, scan demos, calibration-aware analysis, telemetry simulation, history, charts, and safety-first reports.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/spiderzen/src/App.tsx` — routed product experience and local demo state
- `artifacts/spiderzen/src/index.css` — SpiderZen visual system and responsive layout
- `artifacts/spiderzen/public/assets/images/refinery-1.jpg` through `refinery-4.jpg` — reserved paths for the supplied refinery photography
- `artifacts/spiderzen/src/components/error-boundary.tsx` — global recovery screen

## Architecture decisions

- The first build is frontend-only and uses localStorage for demo persistence so the full judgeable flow works without backend setup.
- Quantitative estimation is intentionally safety-aware: without a validated calibration dataset, results remain clearly marked demo, simulated, or estimated.
- The scanner uses the device camera when available and provides upload/demo fallbacks instead of leaving a black screen on permission or hardware failure.
- Refinery photos are loaded from stable public asset paths; missing photos produce an intentional technical fallback rather than a broken hero.

## Product

The app covers the complete prototype journey: industrial context pages, camera/upload/demo strip scanning, analysis and result review, exposure charts, local history, printable/downloadable reports, dataset validation, calibration gating, ESP32 telemetry simulation, exposure simulation, feature discovery, cartridge information, safety guidance, and settings.

## User preferences

The experience should remain mobile-first, touch-friendly, safety-conscious, and explicit about the difference between validated measurements and simulated/demo results.

## Gotchas

- The Vite build requires `PORT` and `BASE_PATH` when run outside the managed workflow.
- The requested refinery photos were not included in the uploaded text brief; add them at the reserved public asset paths to activate the photographic heroes.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
