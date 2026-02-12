# Build plan: QuickBets

## Repo structure
- `/src/app` — Next.js App Router (pages, layout)
- `/src/server` — tRPC context, routers
- `/src/components` — shared UI
- `/src/styles` — Tailwind
- `/prisma` — schema, migrations

## Phases
1. Init repo + deps (Next.js, Prisma, Clerk, tRPC, Tailwind, Sentry, Upstash, Playwright)
2. DB schema + migrations (Neon)
3. Auth (Clerk)
4. tRPC routers (per PRD)
5. UI screens + components (per UX/Frontend blueprint)
6. E2E (Playwright critical flows)
7. Sentry + deployment steps

## No ambiguity
- All choices above are final for this run.
- If multiple options existed, one is chosen; alternatives noted in decisions.


## Council summary
# Council roundtable: QuickBets

## Input idea
prediction market on base with quick fulfillment (short durations like 15mins) social events, esports etc

## PRD-lite
## PRD-lite: QuickBets

### Problem
Users want a fast and engaging way to place bets on social events and esports, but existing platforms often have long wait times and lack the excitement of quick fulfillment. This results in missed opportunities and a less thrilling betting experience.

### Users
- **Casual bettors**: Individuals who enjoy betting on social events and esports but prefer quick and easy transactions.
- **Esports enthusiasts**: Fans who want to engage with their favorite games through betting but are deterred by complex platforms.

### Scope (MVP)
- [ ] Quick bet placement for events with a duration of 15 minutes or less.
- [ ] User-friendly interface for browsing upcoming events.
- [ ] Real-time updates on event status and outcomes.
- [ ] Social sharing features to promote bets among friends.
- [ ] Basic user authentication and account management.
- [ ] Simple payout mechanism for winning bets.
- [ ] Notifications for upcoming events and bet outcomes.

### Out of scope
- Long-term betting options (beyond 15 minutes).
- In-depth analytics or statistics for events.
- Advanced user profiles or social features (e.g., chat).
- Betting on non-social or non-esports events.

### Success criteria
- [ ] At least 500 bets placed within the first month of launch.
- [ ] 80% of users report satisfaction with the speed of bet fulfillment.
- [ ] 70% of users engage with social sharing features.

### Open questions
- [ ] What specific social events will be included in the initial launch?
- [ ] How will we handle regulatory compliance for betting in different regions?
- [ ] What payment methods will be supported?

### Constraints
- Stack: Next.js + TypeScript + Prisma + Neon + Clerk + tRPC + Tailwind + Sentry + Upstash + Playwright.
- Timeline: Launch within 3 months.
- Budget: Defined based on development and marketing needs.

---

## Council sections

### frontend-architect

## Frontend Architecture: QuickBets

### Route tree
/app
├── layout.tsx (root layout)
├── page.tsx (landing)
├── (auth)/
│   ├── sign-in/
│   └── sign-up/
└── (bets)/
    ├── layout.tsx
    ├── upcoming/
    ├── active/
    └── results/

### Key components
| Component                | Type   | Purpose                                      |
|-------------------------|--------|----------------------------------------------|
| BetCard                 | client | Displays individual bet options with quick actions. |
| EventList               | server | Lists upcoming events for betting.          |
| NotificationBanner       | client | Shows real-time updates on event status.    |
| SkeletonLoader          | client | Provides loading states for dynamic content. |
| ErrorBoundary           | client | Catches and displays errors in the UI.      |

### State strategy
- Server state: tRPC + React Query for fetching event 