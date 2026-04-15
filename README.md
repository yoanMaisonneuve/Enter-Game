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

## What this repo contains

- [`README.md`](README.md) — this file (EN)
- [`README.fr.md`](README.fr.md) — French version
- [`PIPELINE.md`](PIPELINE.md) — the full Grain → Action architecture
- [`EXTERNAL-CONDITION-CONTEXT.md`](EXTERNAL-CONDITION-CONTEXT.md) — the interface layer (today: headset; tomorrow: BCI)
- [`LICENSE`](LICENSE) — MIT
- `ideas/` — append-only voice captures from live sessions

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

## Status

- **v1 · April 2026** — structure live, docs published, first real use case (EasyRead + aski01 + private infra)
- Next: bilingual translation of all foundational docs · templates repo · public case studies

Maintainer: [Yoan Maisonneuve](https://github.com/yoanMaisonneuve).

---

*"You don't start a company. You enter the game."*
