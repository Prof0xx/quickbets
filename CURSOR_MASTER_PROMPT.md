# Cursor Master Prompt — QuickBets

Build the following app with **zero ambiguity**. Do not ask for clarification; use the choices below. If something is unspecified here, use the stack defaults and document the choice in a short COMMENT in code or README.

## Idea
prediction market on base with quick fulfillment (short durations like 15mins) social events, esports etc

## Stack (exact)
- **Framework:** Next.js 14+ (App Router), TypeScript
- **DB:** Prisma + Neon (Postgres)
- **Auth:** Clerk
- **API:** tRPC only for app logic
- **UI:** Tailwind CSS
- **Errors/telemetry:** Sentry
- **Rate limit/cache:** Upstash (when needed)
- **E2E tests:** Playwright

## Repo structure
- `/src/app` — App Router pages and layout
- `/src/server` — tRPC context and routers
- `/src/components` — reusable UI
- `/src/styles` — Tailwind
- `/prisma` — schema and migrations

## Database
- Use Prisma with Neon. Define models in `prisma/schema.prisma` per PRD/Backend Architect. Run migrations before deploy.

## APIs
- tRPC only for app logic. Procedures in `/src/server/routers`. Auth via Clerk; pass userId in context. No REST except webhooks/third-party if required.

## UI
- Tailwind. High-end, smooth animations. Every data surface must have: loading state, empty state, error state. Responsive; accessibility (a11y) required.

## Testing
- Playwright E2E for critical flows: sign-in, main user journey, key error paths. No TBD in test list; define exact flows from QA Lead.

## Errors and telemetry
- Sentry for errors. Structured logging for important actions. No secrets in logs.

## Deployment
- Build: `npm run build`. Run migrations before deploy. Document rollback (migrations back, revert deploy). Small diff only when in operator/maintenance mode.

## Rules
- Do not add NFTs or unrelated features.
- Do not leave TBD or "maybe" in implementation; pick one option and note alternatives in comments if needed.
- Stick to this spec; defer to PRD and council outputs in `/vault/business/apps/quickbets/` if present.