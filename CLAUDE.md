# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Arcade Vault: a platform to play games online and compete for the highest score (README is in Spanish). Currently a fresh Create Next App scaffold — only `app/layout.tsx`, `app/page.tsx` and `app/globals.css` exist.

## Commands

- `npm run dev` — dev server
- `npm run build` / `npm start` — production build / serve
- `npm run lint` — ESLint (flat config in `eslint.config.mjs`, `eslint-config-next`)
- No test runner is configured yet.

## Stack notes

- Next.js 16.4 (App Router, `app/` dir), React 19.3, Tailwind CSS v4 (`@import "tailwindcss"` in `app/globals.css`, theme tokens via `@theme inline`), TypeScript with path alias `@/*` → repo root.
- **This Next.js has breaking changes vs. older versions.** `AGENTS.md` requires reading the relevant guide in `node_modules/next/dist/docs/` (`01-app`, `02-pages`, `03-architecture`, `04-community`) before writing Next.js code, and heeding deprecation notices. E.g. the root layout uses the globally-available `LayoutProps<"/">` type rather than importing a props type.

## Spec-driven workflow

The project uses spec-driven development (skills from `inerhead/gossio-skills`, installed in `.agents/skills/` and `.claude/skills/`, locked in `skills-lock.json`):

- `/spec <feature>` — interactively designs a spec (asks clarifying questions first, no code) and saves it to `specs/NN-name.md` using `.agents/skills/spec/template.md`. Specs match the language and conventions of existing ones.
- `/spec-impl <NN-spec-name>` — only runs on specs whose state is "Approved"; creates a git branch named after the spec and implements step by step, pausing for diff review. Branch creation is configurable via `specs/.spec-config.yml` (`AutoCreateBranch`).

For large features, write/approve a spec in `specs/` before coding.
