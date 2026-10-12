# Changelog

## 1.0.0 (2026-10-11)

First public release.

- Phase 0: reads an existing repo (stack, schema, git hot spots, open issues, existing ADRs) before asking questions.
- Phase 1: short interview, 2 or 3 questions per turn, only for what the repo and the user have not already answered.
- Phase 2: defaults table that starts simple (modular monolith, Postgres, managed hosting) and only adds components for a stated reason. Competing designs for decisions that are expensive to reverse. Back-of-envelope sizing.
- Phase 3: blueprint with diagram, components, data model, critical flows, hard problems, cost, roadmap, decision log, and open questions. Scales down for small projects.
- Phase 4: writes `docs/architecture.md` and one ADR per major decision into `docs/adr/`.
