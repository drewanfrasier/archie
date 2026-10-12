# Archie

**A system architecture skill for Claude and other AI coding agents.**

Tell Archie what you want to build. It asks a few sharp questions, then hands you an architecture you can start on tomorrow: stack choices tied to your actual requirements, a data model, the two or three problems that will really hurt, a cost range, and a phased roadmap. If you are in a repo, it reads your code first and writes its decisions back in as ADRs.

```bash
npx skills add drewanfrasier/archie
```

## Why Archie

Most AI architecture advice reaches for Kafka, microservices, and Kubernetes because they sound impressive. Archie does the opposite.

- **Starts simple.** Modular monolith, one Postgres database, managed hosting. Every extra component has to be forced by a requirement you stated, and Archie names that requirement.
- **Every choice is traceable.** Each recommendation points to something you said, something it found in your code, or a labeled assumption, and names the alternative it beat.
- **Reads before it asks.** In an existing repo it looks at your manifests, schema, git hot spots, open issues, and existing ADRs before asking anything.
- **Finds the hard problems.** Double-booking, idempotent payments, offline sync conflicts, tenant data leakage. Archie identifies the two or three that matter for your system and designs for them explicitly.
- **Competes the big decisions.** For choices that are expensive to reverse, it develops two or three genuinely different designs and tells you why the losers lost.
- **Leaves a paper trail.** Writes `docs/architecture.md` and one ADR per decision into `docs/adr/`, and respects ADRs that already exist.
- **Scales to the stakes.** A weekend project gets one page. A funded product with compliance obligations gets the full treatment.

## How it works

| Phase | What happens |
| --- | --- |
| 0. Read | If there is a repo: stack, schema, boundaries, git hot spots, open issues, existing ADRs |
| 1. Discover | 2 or 3 questions per turn, at most 3 rounds, only for what is still unknown. Confirms a short summary before designing |
| 2. Assess | Applies sensible defaults, competes the expensive decisions, sizes load and cost, names what breaks first at 10x |
| 3. Blueprint | Summary, diagram, components, data model, critical flows, hard problems, competing designs, non-functional requirements, cost, roadmap, decision log, open questions |
| 4. Record | Writes the blueprint and ADRs into the repo |

## Example

> **You:** I want to build a cooking app with recipes from every culture. Mobile first, iOS and Android. Recipes come from users and from AI. Freemium. I'm solo and my infra budget is $50 to $300 a month.

Archie asks about scale, how AI recipes get reviewed, and whether offline matters, then delivers a blueprint. An abbreviated excerpt:

> **Summary.** A single React Native app over a modular monolith backend on managed Postgres, with AI generation running as background jobs. This fits a solo developer and a small budget. The biggest risk is AI-generated recipes that are wrong or unsafe reaching users without review.
>
> **Hard problems.**
> 1. *AI recipe quality.* Generated recipes land in a `pending_review` state and are never shown publicly until they pass validation and moderation.
> 2. *Subscription state across two app stores.* Store receipts are verified server side and webhooks are processed idempotently, keyed by transaction ID.
> 3. *Ingredient search across cuisines.* Postgres full-text search with a synonym table to start; a dedicated search engine only if relevance tuning becomes a core feature.
>
> **Roadmap, Phase 1 (MVP).** Browse, search, and save recipes end to end. Nothing else.

## Install

### Any agent (Claude Code, Cursor, Codex, Windsurf, and others)

```bash
npx skills add drewanfrasier/archie
```

Update later with `npx skills update`.

### Claude Code plugin marketplace

```
/plugin marketplace add drewanfrasier/archie
/plugin install archie@archie
```

Archie then runs as `/archie:archie`, or automatically when you ask how to build or structure something.

### claude.ai and Claude Desktop

1. Download `archie.zip` from the [latest release](https://github.com/drewanfrasier/archie/releases/latest).
2. Go to **Settings > Capabilities > Skills** and click **Upload skill**.
3. Select `archie.zip`.

Code execution must be enabled for skills to run.

### Manual

Copy `plugins/archie/skills/archie/` into `~/.claude/skills/` (all your projects) or `.claude/skills/` in one repo.

## Using it

Ask the way you normally would:

- "How should I build a booking platform for dog groomers?"
- "Plan the architecture for this repo before we add multi-tenancy."
- "We're outgrowing our Rails monolith. What should the migration look like?"
- "We're pivoting from a marketplace to a SaaS tool halfway through the MVP. What should we keep?"
- "Revisit the decision in ADR 0003. Our traffic changed."

Say "just pick" at any point and Archie will choose sensible defaults and label them as assumptions.

## Contributing

Issues and pull requests are welcome. If Archie gave you a bad recommendation, open an issue with what you asked and what it said. Those reports are the most useful thing you can send.

## License

[MIT](LICENSE)
