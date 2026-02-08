# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Repository

This is a **documentation-only repository** describing Feature-Action Architecture (FAA) — a backend architecture pattern. There is no source code to build, test, or run. All content is Markdown documentation.

## Repository Structure

| File/Dir | Purpose |
|---|---|
| `README.md` / `README.RU.md` | Main overview, quick start, project structure reference |
| `MANIFEST.md` / `MANIFEST.RU.md` | The philosophical "why" behind FAA, anti-patterns, decision guide |
| `AI.md` | Rules for AI/LLM agents working with FAA codebases |
| `examples/` | Language-specific examples (ts-bun, kotlin-springboot, golang-gin, python-django, csharp-asp) |

## Core Architecture Concepts

FAA is a backend adaptation of Feature-Sliced Design. Key ideas:

**4 Layers (strict top-to-bottom dependency flow only):**
```
App → Features → Entities → Shared
```

- **App** — DI wiring, router, server init
- **Features** — Business use cases (actions + handlers + feature-specific queries)
- **Entities** — Domain data (DB models, CRUD DAL, reusable domain logic)
- **Shared** — Infrastructure and pure utilities

**Critical rules:**
- No horizontal imports (Feature → Feature, Entity → Entity)
- No upward imports (Entity → Feature, Shared → Entity)
- Each feature exposes a public API boundary (`index.ts` in TS/JS, access modifiers in other languages)
- Actions are factory functions receiving explicit dependencies — no hidden globals
- DALs contain only generic CRUD; business logic lives in actions

## When Contributing Documentation

- Maintain bilingual parity: if updating `README.md` or `MANIFEST.md`, update the `.RU.md` counterpart
- The `AI.md` file is the authoritative reference for how AI agents should work with FAA projects
- Examples in `examples/` follow the same structural conventions; keep them consistent with the patterns described in `MANIFEST.md`
