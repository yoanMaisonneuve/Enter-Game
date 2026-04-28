# enter-game

> **You don't start a company. You enter the game.**

An open-source protocol for operating with AI as a permanent co-founder — not a search engine.

🇫🇷 Version française : [README.fr.md](README.fr.md)

---

## Start here

**New?** → [`QUICKSTART.md`](QUICKSTART.md) — setup in under 1 hour.

**Enterprise skills?** → [`skills/`](skills/) — 77+ commands across 7 domains (communication, planning, code, finance, and more).

**Solo founder?** → [`solofounder/`](solofounder/) — 9-department AI OS. CEO to Support, all from a single repo.

**All commands?** → [`COMMANDS.md`](COMMANDS.md) — the full agentic command layer, 7 tiers.

**Web interface?** → [`Jouer.html`](Jouer.html) or `yoanmaisonneuve.github.io/enter-game` (for those who don't navigate GitHub).

---

## Why this exists

Most AI guides teach prompting. This teaches operating.

The difference: prompting is a transaction. Operating is a system. A system has memory, context, protocols, commands, and feedback loops. Once it's running, it compounds.

This repo documents the system — the architecture, the protocols, the traps, the unfair advantages — for anyone who wants to work at the frontier without a team.

---

## The core thesis

> The real bottleneck is not compute. It's the human feeding context to the model.

GPUs are idle most of the day. Models can write code faster than any team. What's slow is the human — deciding what matters, framing the problem, validating the output, committing the result.

If you optimize the human-AI handshake, everything else accelerates.

- RAND 2025: **80–90% of agent projects fail in production** — root cause is almost always bad context.
- Karpathy: **idle tokens mean you are the bottleneck.**
- The winners build systems, not prompts.

---

## The 5 principles — CAPGS

**C — Context first, always.**
No task starts without the right context loaded. A small CONTEXT.md file beats a 10,000-token prompt every time.

**A — Autonomy on tactics, validation on architecture.**
The model runs the details. The human validates the big decisions.

**P — Parallelism by default.**
Batch tasks into a single message. Three sequential prompts = three context loads.

**G — GitHub is the single source of truth.**
Not Notion. Not Google Drive. Not a local folder. Everything ships through Git.

**S — Specificity beats generality.**
A specific prompt with a concrete example beats a generic one every time.

---

## What's in this repo

### Protocol Documents

Six self-contained documents. A fork can reconstruct the full system from these alone.

| Document | What it teaches |
|---|---|
| [`POWERUSER.md`](POWERUSER.md) | State of the art 2026 — the 8 unofficial power-user practices and the N3→N5 progression table. Read this first. |
| [`README_agents.md`](README_agents.md) | The 7-agent pipeline (Planner → Researcher → Analyst → Builder → Reviewer → Archivist → MetaObserver). |
| [`README_memory.md`](README_memory.md) | The 4-layer memory architecture (L1 CONTEXT → L2 RECENT → L3 projects → L4 ARCHIVE) and handoff protocol. |
| [`README_workflow.md`](README_workflow.md) | The temporal protocol: daily execution → weekly review → monthly audit → quarterly direction → annual upgrade. |
| [`README_voicefirst.md`](README_voicefirst.md) | The 5-step voice protocol (input → structuring → dispatch → execution → feedback) and reproducible setup. |
| [`README_flywheel.md`](README_flywheel.md) | The propagation-by-proof distribution mechanism — how each user becomes a distribution node. |

---

### Skills Library — `skills/`

77+ actionable commands mapped to real enterprise use cases. Organized by domain:

| File | Domain | Top commands |
|---|---|---|
| [`01-COMMUNICATION.md`](skills/01-COMMUNICATION.md) | Email, reports, translation | `email-draft`, `email-reply`, `write-report`, `rewrite` |
| [`02-PLANNING.md`](skills/02-PLANNING.md) | Projects, OKRs, retrospectives | `status`, `sprint-plan`, `roadmap`, `retro` |
| [`03-KNOWLEDGE.md`](skills/03-KNOWLEDGE.md) | Research, synthesis, docs | `recherche`, `synthèse`, `brief`, `competitive` |
| [`04-CODE.md`](skills/04-CODE.md) | Dev work, review, incidents | `revue`, `debug`, `spec-tech`, `postmortem` |
| [`05-PEOPLE.md`](skills/05-PEOPLE.md) | HR, feedback, hiring | `job-post`, `feedback`, `1on1`, `pip` |
| [`06-CUSTOMER.md`](skills/06-CUSTOMER.md) | Sales, support, CRM | `outreach`, `sales-proposal`, `battlecard` |
| [`07-FINANCE-OPS.md`](skills/07-FINANCE-OPS.md) | Finance, ops, compliance | `financial-report`, `budget`, `sop` |
| [`08-SHORTCUTS.md`](skills/08-SHORTCUTS.md) | Shorthand protocol | `Git/[project]`, `/[command]`, install in 5 min |

---

### Solo Founder OS — `solofounder/`

One person. Nine departments. Full company operations with AI.

| File | Department | Highlights |
|---|---|---|
| [`01-CEO.md`](solofounder/01-CEO.md) | Direction | `vision`, `priorités`, `pitch`, `north-star` |
| [`02-VENTES.md`](solofounder/02-VENTES.md) | Sales | `lead-scan` (8 sectors), `cold-email`, `close` |
| [`03-MARKETING.md`](solofounder/03-MARKETING.md) | Marketing | `content`, `seo-audit`, `campaign` |
| [`04-PRODUIT.md`](solofounder/04-PRODUIT.md) | Product | `spec`, `roadmap-produit`, `user-story` |
| [`05-TECH.md`](solofounder/05-TECH.md) | Engineering | `architecture`, `debug`, `deploy` |
| [`06-OPERATIONS.md`](solofounder/06-OPERATIONS.md) | Operations | `sop`, `process`, `vendor` |
| [`07-FINANCE.md`](solofounder/07-FINANCE.md) | Finance | `trésorerie`, `budget`, `invoice` |
| [`08-DISTRIBUTION.md`](solofounder/08-DISTRIBUTION.md) | Distribution | `launch`, `channels`, `partenariats` |
| [`09-SUPPORT.md`](solofounder/09-SUPPORT.md) | Support | `ticket`, `faq-gen`, `escalation` |

---

### Templates — `templates/`

Copy-paste starters. Fill the brackets. Works in 15 minutes.

- [`CLAUDE.md`](templates/CLAUDE.md) — your Claude context file (who you are, what you're building, how you work)
- [`CONTEXT.md`](templates/CONTEXT.md) — L1 working memory (< 60 lines)
- [`RECENT.md`](templates/RECENT.md) — L2 episodic memory (last 2–4 weeks)
- [`SHORTCUTS_REGISTRY.md`](templates/SHORTCUTS_REGISTRY.md) — your personal command language (installable in 5 min)

---

### Agentic Layer

- [`QUICKSTART.md`](QUICKSTART.md) — from zero to first session in under 1 hour
- [`COMMANDS.md`](COMMANDS.md) — full command reference, 7 tiers: Core Session, Capture, Build, Plan, Memory, Output, Agent Pipeline

---

### Tools & Infrastructure

- [`index.html`](index.html) — **Enter the Game Hub**, L2.5 idea-capture app (runs on GitHub Pages, pinnable to phone)
- [`Jouer.html`](Jouer.html) — interactive web guide (no GitHub needed)
- [`LEVELS.md`](LEVELS.md) — the 5-level progression (L1 phone → L5 autonomous agents)
- [`PIPELINE.md`](PIPELINE.md) — full Grain → Action architecture
- `ideas/` — append-only voice captures from live sessions
- `Claude_init/` — working memory architecture for Claude (session logs, index, todo)

---

## The pipeline

```
GRAIN → INTERFACE → TRIAGE → MODEL → MEMORY → GLOBAL CONTEXT → ACTION → FEEDBACK
```

See [PIPELINE.md](PIPELINE.md) for the full stage-by-stage breakdown.

---

## The shorthand protocol

After setup, you never explain context twice:

```
Git/Enter-Game          → load Enter-Game context silently. Confirm in 1 line.
Git/Blueprint           → switch to Blueprint project
/vidéo du jour          → scan AI videos, produce digest, save to journal/
/news IA                → morning AI briefing in your format
/standup                → daily standup from recent activity
/handoff                → archive session, update RECENT.md, push
```

Install in 5 minutes. See [`skills/08-SHORTCUTS.md`](skills/08-SHORTCUTS.md).

---

## The command set

| Command | Effect |
|---|---|
| `go [task]` | Execute immediately, no preamble |
| `contexte` | Load CONTEXT.md + RECENT.md, summarize state |
| `handoff` | Archive session + update memory |
| `idée [text]` | Capture idea, push to GitHub |
| `spec [subject]` | Write a PRD/spec |
| `plan [horizon]` | Planning session |
| `interview-moi [X]` | Ask 5–8 questions about blind spots |
| `mémoire [X]` | Save to memory |

Full reference: [`COMMANDS.md`](COMMANDS.md)

---

## How to use this

**Fastest path (< 1 hour):** follow [`QUICKSTART.md`](QUICKSTART.md).

Manual path:
1. **Fork** this repo
2. **Create a private memory repo** (`memory`, `brain`, `<yourname>-memory`)
3. **Copy** `templates/CLAUDE.md`, `templates/CONTEXT.md`, `templates/RECENT.md` into it
4. **Fill your CONTEXT.md** — who you are, what you're building, what's locked
5. **Load it** into your AI tool at session start (paste content, or use Claude Projects)
6. **Say** `contexte` to confirm the state

The protocol is not the point. The practice is.

---

## Who this is for

- **Solo founders** building real products with AI as co-founder
- **Enterprise knowledge workers** who want to reclaim 1–2h/day (see `skills/`)
- **Teams deploying AI** who need a skills layer, not just prompts

---

## The guardrails

| Rule | Threshold |
|---|---|
| Production deploys | Always explicit human confirmation |
| Unplanned spend above $5 | Flag before acting |
| Financial actions (trades, transfers) | Never autonomous — always human |
| `.env` / secrets | Never committed |

---

## Enter the Game · 5 Levels

See [LEVELS.md](LEVELS.md) for the full breakdown.

1. **L1** · Phone + Claude (manual copy-paste)
2. **L2** · GitHub Codespaces (browser IDE)
3. **L2.5** · **Enter the Game Hub** — [`index.html`](index.html), pinnable to phone, push ideas without terminal
4. **L3** · Claude Dispatch (Computer Use, hands-free voice → desktop)
5. **L4** · VPS / OVH cluster (Claude on always-on infra)
6. **L5** · Autonomous agents (scoped mandate + budget cap)

---

## Status

- **v1.0 · April 2026** — structure live, docs published
- **v1.1 · April 2026** — Hub HTML app + LEVELS doc + Pages deployment
- **v1.2 · April 2026** — 6 core protocol documents (POWERUSER + agents + memory + workflow + voicefirst + flywheel)
- **v1.3 · April 2026** — agentic layer: `skills/` (77 commands), `solofounder/` (9 departments), `templates/`, `COMMANDS.md`, `QUICKSTART.md`, `Claude_init/`

Maintainer: [Yoan Maisonneuve](https://github.com/yoanMaisonneuve).

---

## License

MIT — see [LICENSE](LICENSE).

Fork, adapt, reshape. Credit is nice. Obligation is not.

---

*"You don't start a company. You enter the game."*
