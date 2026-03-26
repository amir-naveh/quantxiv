# Current Project Status

**Last updated:** 2026-03-26

---

## What Exists
- `GOAL.md` — project goal and MVP feature list
- `next_step_process.md` — repeating development cycle instructions
- `web/` — Next.js 16 app (TypeScript + Tailwind CSS)
  - Single placeholder page: quantxiv name + tagline
  - Build verified and working

## What Works
- `npm run build` succeeds (webpack mode)
- `npm run dev` will serve the app locally at `localhost:3000`

## What Is Missing (Everything)
- Database (PostgreSQL — not yet set up)
- arxiv paper ingestion (no API integration yet)
- Paper feed UI
- Paper detail page + threaded comments
- User authentication
- Moderation tooling
- Deployment / hosting

## Stack Decisions Made
| Layer | Choice |
|---|---|
| Frontend/Backend | Next.js 16 (App Router, TypeScript) |
| Styling | Tailwind CSS |
| Database | PostgreSQL (not yet configured) |
| Auth | TBD (likely NextAuth.js) |
| Hosting | TBD (likely Vercel + managed Postgres) |

## What Comes Next
Set up the database schema and ORM (Prisma + PostgreSQL) to model the core entities: `Paper`, `User`, `Comment`, `Reaction`.
