# Changelog

## 1.1.0 (2026-10-11)

Pivot support.

- Phase 1 now separates a migration (live product with real users or data: incremental plan, never a big-bang rewrite) from a pivot (direction changed, usually before or shortly after launch).
- New Pivots section in Phase 2: weighs code size, usage, data model fit, and plumbing versus domain logic. Allows a partial rewrite when the MVP is not live, and sorts existing code into keep, adapt, and drop with file paths.
- Roadmap covers pivots: the keep, adapt, and drop list, then ordered steps to the new MVP, with what gets deleted and when.
- A pivot counts as a conflicting requirement for existing ADRs. Affected ADRs are marked Superseded with links to the new ones, never deleted.
- Skill description mentions pivots so Archie triggers on them.

## 1.0.0 (2026-10-11)

First public release.

- Phase 0: reads an existing repo (stack, schema, git hot spots, open issues, existing ADRs) before asking questions.
- Phase 1: short interview, 2 or 3 questions per turn, only for what the repo and the user have not already answered.
- Phase 2: defaults table that starts simple (modular monolith, Postgres, managed hosting) and only adds components for a stated reason. Competing designs for decisions that are expensive to reverse. Back-of-envelope sizing.
- Phase 3: blueprint with diagram, components, data model, critical flows, hard problems, cost, roadmap, decision log, and open questions. Scales down for small projects.
- Phase 4: writes `docs/architecture.md` and one ADR per major decision into `docs/adr/`.
