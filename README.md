# enter-game

> **You don't start a company. You enter the game.**

An open-source protocol for solo founders who build with an AI co-founder.

🇫🇷 Version française : [README.fr.md](README.fr.md)

---

## Why this exists

Most guides for founders are written for teams. Team dynamics, hiring, management, investors.

But a new category exists now: **the solo builder with an AI co-founder**. One human. One model. A GitHub account. A cluster. That's the whole company.

This setup is not "startup lite". It's a different game with different rules — different bottlenecks, different leverage, different failure modes.

`enter-game` documents that game. The protocols, the architecture, the traps, the unfair advantages.

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
No task starts without the right context loaded. A small CONTEXT.md file that the model reads at session start beats a 10,000-token prompt every time.

**A — Autonomy on tactics, validation on architecture.**
The model runs the details. The human validates the big decisions (architecture, production deploys, budget caps).

**P — Parallelism by default.**
Batch tasks into a single message. Three sequential prompts = three context loads. One batched prompt = one load.

**G — GitHub is the single source of truth.**
Not Notion. Not Google Drive. Not a local folder. Everything ships through Git.

**S — Specificity beats generality.**
A specific prompt with a concrete example beats a generic one. Always give the target *and* the anti-target.

---

## Protocol Documents — Start Here / Documents du Protocole — Commencer Ici

Six self-contained documents. A fork of this repo can reconstruct the full system from these six files alone.

| Document | What it teaches |
|---|---|
| [`POWERUSER.md`](POWERUSER.md) | State of the art 2026 — the 8 unofficial power-user practices, the gap between mainstream / advanced / frontier, and the N3→N5 progression table. Read this first. |
| [`README_agents.md`](README_agents.md) | The 7-agent pipeline (Planner → Researcher → Analyst → Builder → Reviewer → Archivist → MetaObserver) — role, inputs, outputs, and activation patterns for each agent. Dev and non-dev branches. |
| [`README_memory.md`](README_memory.md) | The 4-layer memory architecture (L1 CONTEXT → L2 RECENT → L3 projects → L4 ARCHIVE), the upgrade path from basic to hybrid (pgvector + Mem0), and the session handoff protocol. |
| [`README_workflow.md`](README_workflow.md) | The temporal protocol: daily execution → weekly review → monthly audit → quarterly direction → annual upgrade → 5/10/15-year mission. The full CAPS+G principles. |
| [`README_voicefirst.md`](README_voicefirst.md) | The 5-step voice protocol (input → structuring → dispatch → execution → feedback), the two modes (voice-first vs text-first), and a reproducible setup for anyone to implement it. |
| [`README_flywheel.md`](README_flywheel.md) | The propagation-by-proof distribution mechanism — how each user becomes a distribution node, the 4 flywheel components, metrics, and the link to the protocol's deeper mission. |

---

## The pipeline

```
GRAIN → INTERFACE → TRIAGE → MODEL → MEMORY → GLOBAL CONTEXT → ACTION → FEEDBACK
```

See [PIPELINE.md](PIPELINE.md) for the full stage-by-stage breakdown.

The interface today is voice (a headset). See [EXTERNAL-CONDITION-CONTEXT.md](EXTERNAL-CONDITION-CONTEXT.md) for how the interface evolves — and why every improvement in interface bandwidth directly improves the whole system's throughput.

---

## The short command set

A solo builder with a model needs a vocabulary — short, unambiguous commands.

| Command | Effect |
|---|---|
| `go [task]` | Execute |
| `stop` | Halt + save state |
| `status` | Report current state + cost |
| `commit [msg]` | Push to the memory repo |
| `rapport` | Session summary + TODO update + commit |
| `[A] + [B] + [C]` | Batch three tasks in one context window |
| `interview-moi sur [X]` | Ask me 5–8 questions before acting |
| `contexte ?` | Reload memory, summarize state |
| `deploy [app] prod` | Request confirmation, then deploy |

---

## The memory architecture

```
your-memory-repo/  (private)
├── CONTEXT.md          # < 60 lines — loaded every session
├── TODO.md             # live task list
├── DECISIONS.md        # dated log of locked decisions
├── SESSION_LOG.md      # auto session summaries
├── projects/           # one file per active project
├── config/             # infrastructure configs
└── workflow/           # collaboration protocol docs
```

Three layers:
- **L1**: the context file. Tiny. Loaded automatically.
- **L2**: project and infra files. Loaded on demand.
- **L3**: the logs — TODO, DECISIONS, SESSION, ERROR. The living journal.

---

## The guardrails

Non-negotiable. These exist because the model **will** accept a dangerous instruction if you phrase it right. The guardrails are the adult in the room.

| Rule | Threshold |
|---|---|
| Max budget per training session | Hard cap (the model stops itself) |
| Production deploys | Always explicit human confirmation |
| Unplanned spend above $5 | Flag before acting |
| Datasets | Never transmit off the chosen cluster |
| Financial actions (trades, transfers) | Never autonomous — always human |
| `.env` / secrets | Never committed |

---

## Enter the Game · 5 Levels

The protocol ships with a progression — each level removes a layer of friction between an idea and its commit. See [LEVELS.md](LEVELS.md) for the full breakdown.

1. **L1** · Phone + Claude (manual copy-paste)
2. **L2** · GitHub Codespaces (browser IDE)
3. **L2.5** · **Enter the Game Hub** — this repo's [`index.html`](index.html). Published at `yoanmaisonneuve.github.io/enter-game`. Pinnable to your phone home screen. Capture an idea, push to any of your repos, no terminal.
4. **L3** · Claude Dispatch (Computer Use, hands-free voice → desktop)
5. **L4** · VPS / OVH cluster (Claude on always-on infra)
6. **L5** · Autonomous agents (scoped mandate + budget cap)

The game is played at the intersection of two curves — the machine leveling up, and the human learning to delegate. See the *Human Adoption Bottleneck* note in LEVELS.md.

---

## What this repo contains

**Protocol documents (v1.0 — April 2026):**
- [`POWERUSER.md`](POWERUSER.md) — power-user state of the art, 8 unofficial practices, N3→N5 table (EN+FR)
- [`README_agents.md`](README_agents.md) — 7-agent pipeline, full specs, dev + non-dev branches
- [`README_memory.md`](README_memory.md) — 4-layer memory architecture, hybrid upgrade, handoff protocol
- [`README_workflow.md`](README_workflow.md) — daily → 15-year temporal protocol, CAPS+G principles
- [`README_voicefirst.md`](README_voicefirst.md) — 5-step voice protocol, dispatch logic, reproducible setup
- [`README_flywheel.md`](README_flywheel.md) — propagation-by-proof distribution mechanism

**Foundation:**
- [`README.md`](README.md) — this file (EN)
- [`README.fr.md`](README.fr.md) — French version
- [`LEVELS.md`](LEVELS.md) — the 5-level progression (L1 → L5)
- [`PIPELINE.md`](PIPELINE.md) — the full Grain → Action architecture
- [`EXTERNAL-CONDITION-CONTEXT.md`](EXTERNAL-CONDITION-CONTEXT.md) — the interface layer (today: headset; tomorrow: BCI)

**Tools:**
- [`index.html`](index.html) — the **Enter the Game Hub**, L2.5 idea-capture app (runs on GitHub Pages)
- [`LICENSE`](LICENSE) — MIT
- `ideas/` — append-only voice captures from live sessions
- `.github/workflows/pages.yml` — GitHub Pages deployment

---

## Who this is for

- Solo founders shipping real products with an AI co-founder
- Indie hackers moving from "AI as search engine" to "AI as execution layer"
- Builders who want a protocol to steal, fork, and make their own

Not for: corporate product owners looking for a framework. This is ground-floor, voice-first, GitHub-first. Adapt freely.

---

## How to use this

1. **Fork** this repo
2. **Create a private memory repo** (call it whatever — `memory`, `brain`, `<yourname>-memory`)
3. **Copy** the structure from the memory architecture section
4. **Fill your CONTEXT.md** — who you are, what you're building, what's locked
5. **Load it** into your AI tool at session start
6. **Iterate** — every friction point is a candidate for a new protocol entry

The protocol is not the point. The practice is.

---

## License

MIT — see [LICENSE](LICENSE).

Fork, adapt, reshape. Credit is nice. Obligation is not.

---

## Deploying the Hub to GitHub Pages

The `index.html` in this repo is a standalone web app. To make it your always-on capture surface:

1. Go to **Settings → Pages** on your fork
2. Under *Build and deployment*, pick **GitHub Actions** as source (the workflow in `.github/workflows/pages.yml` handles the rest)
3. Wait for the first Action run to finish (green check)
4. Open `https://<yourname>.github.io/enter-game/`
5. Open **Config** tab → paste your GitHub username, a fine-grained PAT with `Contents: write` scope, your repo list, and your author name/email
6. On Android: Chrome → ⋮ → *Add to Home screen*. On iOS: Safari → Share → *Add to Home Screen*. You now have a hub app.

**Security note.** The hub's source code is public. The token is stored only in your browser's `localStorage` — never sent to any third-party server. Still, treat it like a key you've printed on paper: don't screen-share your config tab, and rotate/revoke the PAT any time from `github.com/settings/tokens`.

---

## Status

- **v1 · April 2026** — structure live, docs published, first real use case (EasyRead + aski01 + private infra)
- **v1.1 · April 2026** — Hub HTML app + LEVELS doc + Pages deployment
- **v1.2 · April 2026** — 6 core protocol documents added: POWERUSER + 5 README files (agents, memory, workflow, voicefirst, flywheel)
- Next: templates repo · public case studies · bilingual protocol docs · Enter-Game template repo (fork-and-go)

Maintainer: [Yoan Maisonneuve](https://github.com/yoanMaisonneuve).

---

*"You don't start a company. You enter the game."*
