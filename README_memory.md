# README_memory.md
## Memory Architecture / Architecture Mémoire

**Enter-Game · v1.0 · April 2026**

---

> Your AI is only as good as the context it has.
> This document teaches you how to build memory that compounds — getting richer over time, not noisier.
>
> *Ton IA est aussi bonne que le contexte qu'elle a.
> Ce document t'enseigne comment construire une mémoire qui se capitalise — qui devient plus riche avec le temps, pas plus bruyante.*

---

## TWO READING MODES / DEUX MODES DE LECTURE

| 🛠️ **DEV BRANCH** | 🧭 **NON-DEV BRANCH** |
|---|---|
| pgvector, Mem0, embeddings, conflict resolution, temporal decay | "Your GitHub as your agent's brain" — what to store where and why |

---

## THE CORE INSIGHT / L'INSIGHT CENTRAL

### [NON-DEV]

Most people treat AI memory like a drawer they throw everything into. After a few months, nothing is findable. The context window fills with noise. The agent produces worse results than it did on day one.

The fix is counterintuitive: **memory needs structure AND forgetting**.

Structure tells the agent what matters. Forgetting prevents old information from drowning current context. The four-layer architecture below does both.

---

### [DEV]

The consensus from production practitioners (Karpathy, Zep, Mem0, arXiv 2026):
- RAG alone doesn't scale for agent systems beyond ~200 interactions
- TF-IDF-based retrieval degrades at high volume due to lexical noise
- The standard moving to production: **in-context + vector DB + graph DB + SQL**
- Critical feature: temporal decay + conflict resolution (not just retrieval)

---

## THE 4-LAYER ARCHITECTURE / L'ARCHITECTURE 4 COUCHES

```
┌─────────────────────────────────────────────────────────────┐
│  L1 — CONTEXT.md          "Working memory / RAM"           │
│  < 60 lines · Loaded every session · Never stale           │
├─────────────────────────────────────────────────────────────┤
│  L2 — RECENT.md           "Recent episodic memory"         │
│  Last 2–4 weeks · High-density digest · Updated weekly     │
├─────────────────────────────────────────────────────────────┤
│  L3 — projects/           "Long-term project context"      │
│  One file per active project · Loaded on demand            │
├─────────────────────────────────────────────────────────────┤
│  L4 — ARCHIVE/            "Cold storage"                   │
│  Completed projects · Old decisions · Accessible on query  │
└─────────────────────────────────────────────────────────────┘
         │ sits above all four layers:
         ▼
   GLOBAL-PLAN.md          "Directional north star"
   (mission · 5/10/15-year vision · never changes session to session)
```

---

## LAYER-BY-LAYER GUIDE / GUIDE COUCHE PAR COUCHE

---

### L1 — CONTEXT.md

**[NON-DEV]:** This is the one file your AI reads at the start of every session. It must be < 60 lines. If it grows beyond that, you've mixed up what belongs in L1 vs L2. Think of it as the briefing you'd give a new contractor on day one — only the facts they need to not waste time.

**[DEV]:** Loaded into system prompt or as first user message at session start. Cached in Claude Projects or equivalent. Must remain under token budget constraints for reliable loading.

**Required sections:**
```markdown
# [Your name] — Context

## Who I am
[1 line: role, location, what you're building]

## Active projects
- [Project]: [one-line status + next action]

## Locked decisions (never re-discuss)
- [Infrastructure choice, budget limits, architectural decisions]

## Communication shortcuts
- [Your command vocabulary — "go", "batch", "interview-me on X", etc.]

## Current focus (updated each session)
- [Top 1–2 priorities this week]
```

**What does NOT belong in L1:**
- Detailed project specs → L3
- Historical decisions → DECISIONS.md
- Research findings → L3 or L4
- Session notes → RECENT.md

---

### L2 — RECENT.md

**[NON-DEV]:** A rolling digest of the last 2–4 weeks. High-density, no fluff. It answers: "What has happened recently that the agent should know before diving in?" It's the bridge between L1 (permanent context) and L3 (project details).

**[DEV]:** Updated by the Archivist agent at the end of each week or significant session. Rolling window: entries older than 4 weeks get promoted to L3 (if still relevant) or archived to L4 (if closed).

**Template:**
```markdown
# RECENT.md — [Date range]

## Key decisions (last 2 weeks)
- [YYYY-MM-DD]: [Decision] — Reason: [why]

## Completed milestones
- [Project]: [What was shipped/resolved]

## Active threads (in progress)
- [Project/thread]: [Status] — Next: [action]

## Risk flags
- [Risk]: [Status] — Mitigation: [what's in place]

## Context changes
- [Any change to locked decisions, team, infrastructure, etc.]
```

---

### L3 — projects/

**[NON-DEV]:** One markdown file per active project. Loaded on demand when you're working on that project. Contains everything the agent needs to work on that project without asking you to re-explain it.

**[DEV]:** Loaded via context injection at session start when project is active. Structure standardized across all project files for consistent Archivist behavior.

**Per-project file template:**
```markdown
# [Project Name]

## What it is
[1–2 sentences. What problem it solves, for whom.]

## Current state
[Status: dev / testing / live / paused]

## Stack
[Key technologies, services, constraints]

## Active tasks
- [ ] [Task] — [owner: AI / human] — [deadline if any]

## Known issues
- [Issue]: [Workaround or fix status]

## Key decisions (project-specific)
- [Decision]: [Reasoning]

## Next actions
1. [Immediate next step]
2. [Following step]

## Links
- Repo: [URL]
- Docs: [URL]
- [Other relevant links]
```

---

### L4 — ARCHIVE/

**[NON-DEV]:** Long-term cold storage. Completed projects, old decisions, resolved issues. You don't load it every session — you query it when you need to look something up. The Archivist keeps it clean.

**[DEV]:** Structured as monthly files (ARCHIVE/YYYY-MM.md) or per-project archives. Accessible via semantic search (vector DB query) or direct file reference. Never purged — only appended.

**Archival convention:**
```
ARCHIVE/
├── 2026-04.md       # Monthly digest
├── 2026-03.md
├── projects/
│   └── [closed-project].md   # Full project archive on completion
└── decisions/
    └── [major-decision].md   # Full reasoning for significant calls
```

---

## THE HYBRID UPGRADE / L'UPGRADE HYBRIDE

### [NON-DEV] When to upgrade / Quand upgrader

A markdown-only memory system works well up to ~200 sessions and ~20 active projects. After that, two problems emerge:
1. **Retrieval noise**: TF-IDF (keyword search) generates false positives — wrong files loaded
2. **Scale**: too many files to scan, context window fills with irrelevant content

The upgrade path: **markdown layer stays (L1–L4) + semantic search layer added underneath**.

---

### [DEV] The Hybrid Memory Stack

**When to implement:** Before hitting 500 sessions or 50 projects.

**Stack:**

```
Layer          Technology              Cost            When
─────────────────────────────────────────────────────────────
In-context     GitHub files (L1–L4)    Free            Always
Vector DB      pgvector on Supabase    Free tier       > 200 sessions
Graph DB       Mem0 (managed)          $15/mo          > 500 sessions
SQL (facts)    Supabase Postgres       Free tier       > 50 decisions
```

**pgvector setup (Supabase):**
```sql
-- Enable pgvector extension
CREATE EXTENSION IF NOT EXISTS vector;

-- Memory table
CREATE TABLE memories (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  content     TEXT NOT NULL,
  embedding   VECTOR(1536),
  layer       TEXT CHECK (layer IN ('L1','L2','L3','L4')),
  project     TEXT,
  created_at  TIMESTAMPTZ DEFAULT NOW(),
  last_access TIMESTAMPTZ,
  relevance   FLOAT DEFAULT 1.0   -- temporal decay applied here
);

-- Semantic search function
CREATE OR REPLACE FUNCTION search_memories(query_embedding VECTOR(1536), match_count INT)
RETURNS TABLE(id UUID, content TEXT, similarity FLOAT)
AS $$
  SELECT id, content, 1 - (embedding <=> query_embedding) AS similarity
  FROM memories
  ORDER BY embedding <=> query_embedding
  LIMIT match_count;
$$ LANGUAGE sql;
```

**Mem0 integration:**
```python
from mem0 import Memory

m = Memory()

# Add memory from session
m.add("Decided to use OVH Beauharnois as primary GPU cluster, budget max $20 CAD/session", 
      user_id="yoan")

# Retrieve relevant context
results = m.search("GPU cluster configuration", user_id="yoan")
```

**Temporal decay function:**
```python
import math

def decay_relevance(base_relevance: float, days_since_access: int, 
                    half_life_days: int = 30) -> float:
    """Exponential decay — relevance halves every `half_life_days` days."""
    return base_relevance * math.exp(-0.693 * days_since_access / half_life_days)
```

**Conflict resolution (Mem0 pattern):**
```
IF new_memory contradicts existing_memory:
  → compare timestamps
  → newer memory wins IF same context (same project, same decision)
  → both preserved IF different context
  → flag for human review IF contradiction is strategic
```

---

## MEMORY COMMANDS / COMMANDES MÉMOIRE

These are the commands your AI understands for memory operations.

| Command | Action |
|---------|--------|
| `context?` | Load and summarize all active context (L1 + L2 + active L3) |
| `archive [X]` | Move X to L4 archive |
| `promote [X] to L1` | Move X to CONTEXT.md (locked decision) |
| `commit` | Commit all memory updates to GitHub |
| `memory health` | Run Archivist check: stale files, bloated layers, conflicts |
| `handoff` | Run full session handoff protocol (see below) |
| `what do you know about [X]?` | Query across all memory layers |

---

## SESSION HANDOFF PROTOCOL / PROTOCOLE DE HANDOFF DE SESSION

**[NON-DEV]:** This is what happens at the end of every significant session. The Archivist runs it. Without it, context degrades over time — each session starts a little less informed than the last.

**[DEV]:** Triggered by explicit `handoff` command or by MetaObserver at session end.

```markdown
# Handoff Protocol — Archivist

Step 1: CAPTURE
→ List all decisions made this session
→ List all tasks completed
→ List all tasks started but not completed

Step 2: CLASSIFY
For each item:
→ Is it a locked decision? → CONTEXT.md (L1)
→ Is it recent context (< 4 weeks)? → RECENT.md (L2)
→ Is it project-specific? → projects/[project].md (L3)
→ Is it completed/historical? → ARCHIVE/ (L4)
→ Is it superseded? → DISCARD

Step 3: UPDATE
→ Write changes to appropriate files
→ Commit to GitHub

Step 4: BRIEF NEXT SESSION
Generate 3-line session opener:
"Last session: [what was accomplished].
Active: [current state of top project].
Next: [top priority for next session]."
```

---

## MEMORY ANTI-PATTERNS / ANTI-PATTERNS MÉMOIRE

### What degrades memory quality / Ce qui dégrade la qualité

| Anti-pattern | Problem | Fix |
|---|---|---|
| Everything in CONTEXT.md | L1 becomes bloated, key facts buried | Strict < 60 line rule |
| Never archiving | Old context clutters active layers | Weekly Archivist run |
| Duplicate entries | Conflicting information, confusion | Archivist deduplication |
| No timestamps | Can't determine freshness | Always date entries |
| Vague entries | Agent can't extract actionable info | Be specific: "Decided X because Y" |

### The golden rule of memory / La règle d'or de la mémoire

> **Memory that is accessible is not necessarily useful. Useful memory is specific, dated, and linked to a decision or action.**

---

## WHAT GOOD MEMORY LOOKS LIKE / À QUOI RESSEMBLE UNE BONNE MÉMOIRE

```markdown
# CONTEXT.md — Yoan Maisonneuve (example)

## Who I am
Solo founder, Lorraine QC. Building Enter-Game + Blueprint system.
Voice-first workflow from earbuds.

## Active projects
- Enter-Game: public repo being built — current task: generate 7 README files
- EasyRead: mobile app — ready to publish, needs GitHub push first
- Blueprint/aski01: civilizational direction system — active, evolving

## Locked decisions
- GPU: OVH Beauharnois (ca-east-bhs). Secondary: Vast.ai CA filter.
- Budget per GPU session: $20 CAD max. Alert at $18.
- Memory: GitHub as source of truth. Never locked in session.
- Voice: default interface. Responses: concise, actionable.

## Shortcuts
- "go [X]" → execute immediately
- "[A] + [B] + [C]" → batch in one context window
- "interview-moi sur [X]" → 5–8 questions before executing
- "rapport" → summary + TODO update + commit
```

This is what 60 lines of effective L1 memory looks like. The agent starts every session knowing exactly who you are, what's active, and how you work.

---

*Enter-Game · README_memory.md · v1.0 · April 2026*
