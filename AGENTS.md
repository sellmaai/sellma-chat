# Repository Guidelines

## Project Structure & Module Organization
The app follows Next.js App Router conventions. Route handlers, layouts, and server actions live under `app/`, with `app/(auth)` and `app/(chat)` grouping auth flows and conversational surfaces. Shared UI is in `components/`, while reusable logic sits in `hooks/` and utilities in `lib/`; database helpers and migrations live in `lib/db/` alongside `drizzle.config.ts`. Static assets are stored in `public/`, and end-to-end specs are collected under `tests/`. Configuration for telemetry, middleware, and Vercel deployment resides at the repo root (`instrumentation.ts`, `middleware.ts`, `vercel-template.json`).

## Build, Test, and Development Commands
Use `pnpm dev` for the turbo-charged Next.js development server, and `pnpm build` to run database migrations (`tsx lib/db/migrate`) before creating the production bundle. `pnpm start` serves the built app, while `pnpm test` executes Playwright suites (requires `PLAYWRIGHT=True`). Run static checks with `pnpm lint` and auto-fix style issues with `pnpm format`. Database maintenance helpers include `pnpm db:generate` for Drizzle typings, `pnpm db:migrate` to apply local migrations, and `pnpm db:studio` for schema inspection.

## Coding Style & Naming Conventions
The project uses TypeScript, React 19 RC, and Tailwind utilities. Maintain 2-space indentation, prefer named exports for shared modules, and keep file names kebab-case (`chat-panel.tsx`) or PascalCase for components. Formatting is enforced by Ultracite + Biome (`biome.jsonc`); always run `pnpm format` before opening a pull request. Co-locate feature-specific styles in module-level CSS, and avoid inline secrets—load environment variables through Next.js runtime configs.

## Testing Guidelines
Playwright drives E2E coverage; place specs in `tests/` and name them with the feature focus (`chat-auth.spec.ts`). Group fixtures per feature and rely on `tests/utils` helpers when adding new suites. Aim to cover primary chat flows (sign-in, prompt submission, transcript persistence) before merging. Execute `pnpm test -- --headed` for interactive debugging and seed any required data using the Drizzle migrations.

## Commit & Pull Request Guidelines
Follow the repository’s short, present-tense commit style (`update dependencies`, `add chat toolbar`). Scope commits narrowly and mention relevant folders when helpful. Pull requests should include a concise summary, testing evidence (`pnpm test` output or screenshots), and links to tracking issues. Capture schema updates by attaching generated SQL diffs, and note any environment variable changes in the PR body.
