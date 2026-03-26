# Coding Guidelines

These guidelines govern all code written in this project. Follow them strictly and consistently across every file, every session.

---

## 1. General Principles

- **Simplicity over cleverness.** Write the simplest code that correctly solves the problem. If you need a comment to explain what code does, rewrite the code first.
- **One thing at a time.** Each function does one thing. Each file owns one concern. Each PR advances one goal.
- **No speculative code.** Do not build for hypothetical future requirements. Build only what is needed now. Abstractions are earned, not anticipated.
- **Consistency is non-negotiable.** Follow the established pattern in the codebase even if you think a different approach is better. Raise it as a suggestion, don't unilaterally deviate.

---

## 2. TypeScript

- **Strict mode always.** `"strict": true` in `tsconfig.json`. Never disable strict checks.
- **No `any`.** Use `unknown` and narrow it, or define a proper type. `any` is a bug waiting to happen.
- **Explicit return types on all exported functions.** Inference is fine internally; exported interfaces must be explicit.
- **Types over interfaces for data shapes; interfaces for contracts.** Use `type` for plain data objects, `interface` when defining a shape that may be implemented or extended.
- **Avoid type assertions (`as X`).** If you need to assert a type, something is wrong with the data flow. Fix the root cause.
- **Enums are forbidden.** Use `as const` objects or union string literals instead. Enums compile poorly and behave unexpectedly.

---

## 3. Project Structure

```
web/
  app/                  # Next.js App Router — pages and layouts only
    (routes)/           # Route groups for logical separation
  components/           # Reusable UI components
    ui/                 # Primitive/atomic components (Button, Input, etc.)
  lib/                  # Shared utilities, helpers, constants
  db/                   # Database client, schema, migrations (Prisma)
  services/             # Business logic and external API integrations
  types/                # Shared TypeScript types and interfaces
```

- **No logic in page files.** Pages (`app/**/page.tsx`) are layout and composition only. Business logic lives in `services/`, data access in `db/`.
- **No cross-layer imports.** `components/` must not import from `services/`. `services/` must not import from `components/`. Data flows down.
- **Co-locate tests.** Unit tests live next to the file they test (`foo.ts` → `foo.test.ts`).

---

## 4. React & Next.js

- **Server Components by default.** Only add `"use client"` when the component genuinely requires browser APIs or interactivity. Document why.
- **No prop drilling beyond 2 levels.** If a prop passes through more than 2 components without being used, introduce context or lift state.
- **No inline styles.** All styling via Tailwind utility classes. Never use `style={{}}`.
- **All images via `next/image`.** Never use raw `<img>` tags.
- **All internal links via `next/link`.** Never use raw `<a>` tags for internal navigation.
- **Loading and error states are required.** Every data-fetching route must have a `loading.tsx` and `error.tsx` sibling.

---

## 5. API Design

- **RESTful routes in `app/api/`.** Name routes after resources, not actions: `/api/papers`, not `/api/getPapers`.
- **HTTP methods map to actions:** GET = read, POST = create, PATCH = partial update, DELETE = remove. Never use GET for mutations.
- **Always return consistent response shapes:**
  ```ts
  // Success
  { data: T }
  // Error
  { error: { message: string; code: string } }
  ```
- **Validate all inputs at the boundary.** Use `zod` for runtime validation on every API route. Never trust incoming data.
- **Never expose internal errors to clients.** Log the real error server-side, return a safe generic message to the client.

---

## 6. Database (Prisma)

- **Schema is the source of truth.** All data shape decisions start in `schema.prisma`, not in application code.
- **Every migration is reviewed before applying.** Never run `prisma migrate deploy` on a schema change without reading the generated SQL.
- **No raw SQL unless absolutely necessary.** If Prisma's query API cannot express the query cleanly, document why raw SQL was needed.
- **Soft deletes for user-generated content.** Add `deletedAt DateTime?` rather than physically deleting comments, papers, or user records.
- **Index every foreign key and every field used in a `where` clause.** Performance issues from missing indexes are avoidable.

---

## 7. Authentication & Security

- **Never store plaintext secrets.** All secrets in environment variables, never committed to git.
- **`.env.local` is gitignored.** Provide a `.env.example` with all required keys and placeholder values.
- **Validate session on every protected route.** Never assume a user is authenticated based on client-side state alone.
- **Sanitize all user-generated content before rendering.** Prevent XSS by treating all user input as untrusted.
- **Rate-limit all public API endpoints.** Especially auth, comment submission, and any search endpoints.

---

## 8. Error Handling

- **Errors are first-class.** Every function that can fail must account for failure in its return type or throw explicitly.
- **Never silently swallow errors.** No empty `catch` blocks. At minimum, log the error.
- **Use structured logging.** Log objects, not strings: `logger.error({ event: 'paper_fetch_failed', paperId, error })`.
- **User-facing errors must be human-readable.** Technical details go to logs, not to the UI.

---

## 9. Testing

- **Test behavior, not implementation.** Tests should break when behavior changes, not when internal code is refactored.
- **Three test levels:**
  - Unit: pure functions and utilities
  - Integration: API routes and database queries (against a real test DB)
  - E2E: critical user flows (paper feed, comment submit, login)
- **No mocking the database in integration tests.** Use a dedicated test database. Mocks hide real failures.
- **Tests must pass before any commit.** A failing test is a blocker, not a warning.

---

## 10. Git & Version Control

- **Commits are atomic.** One logical change per commit. Do not bundle unrelated changes.
- **Commit messages are imperative present tense:** `Add paper feed route`, not `Added paper feed route` or `Adding paper feed route`.
- **No commented-out code in commits.** Delete it. Git history preserves it if needed.
- **`main` is always deployable.** Never commit broken or half-finished code to `main`. Use feature branches for work in progress.
- **`.gitignore` must cover:** `node_modules/`, `.next/`, `.env*.local`, build artifacts.

---

## 11. Claude-Specific Rules

These rules address patterns that AI-generated code commonly gets wrong:

- **Do not invent APIs.** Only use libraries, functions, and APIs that are confirmed to exist. When uncertain, verify before using.
- **Do not add unrequested features.** Scope is sacred. Build what was asked for.
- **Do not silently change existing patterns.** If a better approach exists, implement the current task the established way and note the suggestion separately.
- **Read before editing.** Always read the full file before making changes to it. Never make blind edits.
- **One step at a time.** Complete and verify each step before starting the next. Do not speculatively scaffold multiple layers at once.
- **If something is unclear, ask.** A wrong assumption written into code costs more to fix than a clarifying question costs to ask.
