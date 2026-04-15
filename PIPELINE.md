# Pipeline
## Version 1.2 · April 2026
## The complete flow from Grain to Action

---

## Overview

This file describes the full pipeline that connects Yoan's brain (vision, intention, direction) to real-world execution across all projects.

It is the **operating architecture** of how Yoan works — not a metaphor, but a literal system description.

---

## The Pipeline

```
GRAIN → HEADSET → MODE SWITCH → TRIAGE → CLAUDE (openClaude) → blueprint-memory → GLOBAL CONTEXT → ACTION → FEEDBACK
  [1]      [2]        [2.5]       [2.6]        [3]                    [4]                [5]           [6]       [7]
```

---

## Stage 1: Grain
**What it is:** Raw thought. Vision. Direction. Intention.

Yoan is a visionary. The grain is the starting point — an unformed idea, a strategic direction, a decision, a task. It exists in the brain before any tool touches it.

- Source: Yoan's mind
- Form: Unstructured thought
- Output: Spoken word (via headset) or written command
- Constraint: Sequential — one grain at a time in current setup

---

## Stage 2: Headset Interface
**What it is:** The external brain chip. Current hardware bridge.

See: `EXTERNAL-CONDITION-CONTEXT.md` for full specs.

- Input: Voice from Yoan
- Output: Text to Claude / Audio back to Yoan
- Latency: 100–300ms
- Bandwidth: Low (voice-only, sequential)
- Role: Translates biological signal (voice) into digital input

---

## Stage 2.5: Mode Switch Layer
**What it is:** The transition point between voice-only and screen-required operations.

Not every grain can be fully executed in audio mode. This stage determines which mode is needed before Claude acts.

| Mode | When to use | Examples |
|------|-------------|---------|
| **Voice-only** | Thinking, planning, quick tasks, updates | "status", "add to to do", "what's next" |
| **Screen required** | File creation, repo setup, code review, uploading files | Creating Pipeline.md, uploading GitHub token, reviewing code |

**Current limitation (April 2026):** Claude.ai audio mode cannot create or save real files. Yoan must exit audio mode and switch to text/screen mode to convert voice sessions into actual artifacts.

**Protocol:**
- Claude flags when a task requires screen mode: *"This requires screen mode — exit audio when ready"*
- Yoan switches to screen, confirms, Claude executes
- Return to voice mode when done

---

## Stage 2.6: Triage Layer
**What it is:** Routing logic — not every grain needs the full pipeline.

Before loading full context and memory, Claude determines the weight of the request:

| Tier | Description | Pipeline depth | Examples |
|------|-------------|----------------|---------|
| **Quick** | Simple answer, no memory needed | Stage 1→3→6 | "What's the difference between Opus and Sonnet?" |
| **Standard** | Task execution, project context needed | Stage 1→5→6 | "Update the to do list", "write this file" |
| **Deep** | Major decision, full context + memory | Full pipeline | Architecture decisions, new project setup, training runs |
| **Multi-project** | Affects 2+ projects | Full pipeline + explicit routing | Changes to CONTEXT.md, GPU infra decisions |

**Multi-project routing rule:** When a grain could affect multiple projects, Claude loads Global Context first, identifies all affected projects, then executes in priority order.

---

## Stage 3: Claude in openClaude
**What it is:** The AI processing layer. Co-founder. Executor.

Claude runs inside the **openClaude project** in Claude.ai. This gives it:
- Persistent project files (CONTEXT.md, Pipeline.md, this file)
- Cached context across sessions
- Access to uploaded credentials and config files

**What Claude does here:**
- Interprets the grain
- Reformulates if needed (prompt orchestration via internal script, not multi-agent)
- Routes to the right action
- Executes technical tasks (code, deploy, document, plan)
- Reads/writes to blueprint-memory when needed

**Model:** Claude Sonnet (sweet spot — fast + capable)
**Architecture:** Single model, prompt orchestration. No multi-agent overhead.

---

## Stage 4: blueprint-memory
**What it is:** The external persistent memory layer.

A private GitHub repo (`blueprint-memory`) that stores:

```
blueprint-memory/
├── CONTEXT.md          # Master context — loaded every session
├── TODO.md             # Live task list
├── DECISIONS.md        # Dated log of major decisions
├── SESSION_LOG.md      # Auto-generated session summaries
├── projects/           # Per-project files
├── config/             # OVH cluster config, Dockerfiles, cost monitor
└── workflow/           # WORKFLOW.md — protocol docs
```

**Role in pipeline:**
- Gives Claude memory across sessions (Claude has no native memory between sessions)
- Source of truth for all decisions and project state
- Synced via GitHub — version controlled

**Access:** Claude reads these files when loaded into openClaude project. Writes back via commit commands.

---

## Stage 5: Global Context
**What it is:** The navigation layer across all projects, all time horizons.

The global context file (stored in openClaude + blueprint-memory) contains:

- **Cloud setup parameters** — OVH BHS cluster specs, GPU config, cost limits
- **Active projects** — Blueprint/aski01, EasyRead, enter-game, blueprint-memory
- **Goal map** — objectives across sectors and time horizons
- **Decision log** — locked decisions that never get re-discussed

### Time Horizons

| Horizon | Scope | Examples |
|---------|-------|---------|
| Immediate | Days | Push EasyRead to GitHub, create repos |
| Short-term | Weeks | Publish EasyRead, set up OVH cluster |
| Medium-term | Months | Blueprint scaling US/FR/DE/BR |
| Long-term | Years | Civilizational-scale impact with aski01 |

---

## Stage 6: Action
**What it is:** Real-world execution. The output of the pipeline.

Actions include:
- Code written and deployed
- GitHub repos created and pushed
- Apps published (Google Play, App Store)
- GPU clusters spun up and trained
- Documents, READMEs, protocols created
- External systems triggered (Supabase, Stripe, Docker, Kubernetes)

### Training Job Flow (OVH BHS)
Training runs are a special action category with their own sub-pipeline:

```
"go training" → spin up OVH H100 → launch job → monitor cost → checkpoint → spin down
```
- Budget gate: alert at 18$ CAD, hard stop at 20$ CAD
- Dataset stays on OVH BHS — never transmitted without explicit approval
- Models: Wan2.1, CogVideoX, custom fine-tunes

---

## Stage 7: Feedback Loop
**What it is:** Every action feeds back into the system.

- **Success** → update blueprint-memory, mark TODO done, inform next grain
- **Failure** → log error, identify stage where it broke, propose fix, re-route
- **Unexpected output** → flag to Yoan, await direction before proceeding

**Error routing by stage:**

| Failure point | Response |
|---------------|---------|
| Headset transcription error | Ask Yoan to repeat or switch to text |
| Mode switch missed | Claude flags: "this needs screen mode" |
| Wrong triage tier | Escalate to next tier, reload context |
| Claude execution error | Log, retry once, then surface to Yoan |
| blueprint-memory out of sync | Flag, request manual sync before proceeding |
| GPU cost overrun | Hard stop, save checkpoint, notify Yoan |

---

## Token Efficiency

**Architecture decision:** Single model + prompt orchestration (no multi-agent).

Multi-agent consumes tokens at every step. This pipeline uses:
- One Claude instance
- Internal prompt reformulation before sending (orchestrator script, not separate model)
- Batching: multiple tasks in one context window = one token load

**Rule:** Never split into separate messages what can be batched into one.

---

## Pipeline Health Metrics

| Metric | Target | Current |
|--------|--------|---------|
| Grain → Action latency | <5min for standard tasks | ~2–10min |
| Context load time | <30s | ~10s (cached) |
| Token waste | Minimal | Low (single model) |
| Memory persistence | Full | Partial (manual upload) |
| Headset bandwidth | Voice-only | Voice-only |

---

## Known Bottlenecks (April 2026)

1. **Headset bandwidth** — voice-only, sequential. One thought at a time.
2. **Audio mode file creation** — Claude.ai audio mode cannot create real files. Must exit to screen mode.
3. **Manual memory sync** — blueprint-memory not yet auto-synced. Requires manual commit.
4. **GitHub token** — not yet uploaded to openClaude. Blocks automated repo operations.
5. **No auto-upload** — Claude cannot push files to project autonomously yet.
6. **No training pipeline active** — OVH account not yet created. GPU infra decided but not live.

---

## Document Quality Protocol

Every document created in this pipeline goes through a minimum iteration cycle before being considered complete.

### The Rule

> After every document is created, Claude asks: **"Have you thought of everything?"**
> Yoan can pass or iterate. If the document is critical, a second pass is mandatory.

### Document Tiers

| Tier | Definition | Minimum iterations | Examples |
|------|------------|--------------------|---------|
| **Standard** | Operational docs, notes, logs | 1 pass + 1 review question | Session notes, quick plans |
| **Critical** | Architectural docs, protocols, permanent reference files | 2 passes mandatory | CONTEXT.md, Pipeline.md, ERROR-LOG.md, WORKFLOW.md |
| **Foundational** | Defines how the entire system works | 3 passes + Yoan explicit approval | Pipeline.md, Global Context, Enter-game README |

### Iteration Flow

```
Claude creates document
        ↓
Claude asks: "Have you thought of everything?"
        ↓
Yoan: Pass → document saved as-is
Yoan: Iterate → Claude updates, asks again
        ↓
[If Critical tier] → second pass is mandatory regardless of first answer
        ↓
Document finalized → committed to blueprint-memory
```

### What "Have you thought of everything?" covers

Claude self-checks before asking:
- Missing fields or sections?
- Edge cases not handled?
- Assumptions not documented?
- Future states not anticipated?
- Links to other documents missing?
- Update protocol defined?

Claude surfaces gaps proactively — the question is not just a formality. It is an active audit.

### Current document status

| Document | Tier | Passes completed | Status |
|----------|------|-----------------|--------|
| EXTERNAL-CONDITION-CONTEXT.md | Critical | 1 | ✅ Ready |
| PIPELINE.md | Foundational | 3 | ✅ Ready |
| ERROR-LOG.md | Critical | 2 | ✅ Ready |

---

## Evolution Path

As the External Condition Context evolves (better hardware, neural interfaces), this pipeline evolves with it. Higher bandwidth input → richer grains → faster execution → more parallel action streams.

The pipeline is designed to **scale with the interface**, not be constrained by it.

---

*Last updated: April 14, 2026 · v1.2 · Yoan Maisonneuve · openClaude project*
