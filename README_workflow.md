# README_workflow.md
## The Enter-Game Temporal Protocol / Le Protocole Temporel Enter-Game

**Enter-Game · v1.0 · April 2026**

---

> A solo founder with a great AI and no workflow is still reactive.
> This document gives you the temporal structure that turns daily execution into long-term compounding.
>
> *Un solo founder avec une excellente IA et aucun workflow reste réactif.
> Ce document te donne la structure temporelle qui transforme l'exécution quotidienne en capitalisation à long terme.*

---

## TWO READING MODES / DEUX MODES DE LECTURE

| 🛠️ **DEV BRANCH** | 🧭 **NON-DEV BRANCH** |
|---|---|
| Automation scripts, cron jobs, GitHub Actions, MetaObserver scheduling | CEO mindset daily rhythm, what to do when, why |

---

## THE TEMPORAL MAP / LA CARTE TEMPORELLE

```
DAILY          → Execute. Context load → batch → validate → handoff.
WEEKLY         → Review. TODO update, RECENT.md digest, MetaObserver scan.
MONTHLY        → Audit. Architecture health, memory cleanup, level check.
QUARTERLY      → Strategize. Direction review, N-level assessment.
ANNUAL         → Rethink. Full system upgrade if warranted.
5 / 10 / 15y   → Navigate. Global-Plan alignment, civilizational direction check.
```

Each temporal layer feeds the next. The daily session is how you move. The annual review is how you know you're moving in the right direction.

---

## DAILY PROTOCOL / PROTOCOLE QUOTIDIEN

### [NON-DEV] Your CEO Rhythm / Ton Rythme de PDG

A well-run daily session has four phases:

**Phase 1 — Load (2 minutes)**
Say: *"context?"*
The agent reads CONTEXT.md + RECENT.md and confirms active state. You don't explain anything. You don't re-introduce yourself. You start from current state.

**Phase 2 — Declare (30 seconds)**
Say what you're doing today. Max 3 priorities. If you have more than 3, you need to drop something.

**Phase 3 — Execute (as long as needed)**
Work in batches. 3 tasks? Batch them in one prompt. New decision needed? Use interview rule first. Don't make architectural decisions without asking 5–8 questions.

**Phase 4 — Handoff (5 minutes)**
Say: *"handoff"*
The Archivist runs: decisions logged, RECENT.md updated, commit to GitHub.

**Rule: no session ends without a handoff.**

---

### [DEV] Daily Automation

**Session start script (n8n webhook or Claude Projects auto-loading):**
```
On session init:
1. Read CONTEXT.md → inject into system prompt
2. Read RECENT.md → inject as second context block
3. If active project specified: read projects/[project].md
4. Output: "Loaded. [3-line state summary]. What are we doing today?"
```

**End-of-day commit hook:**
```bash
#!/bin/bash
# Daily commit — runs on handoff command
DATE=$(date +%Y-%m-%d)
cd ~/your-memory-repo
git add -A
git commit -m "daily: $DATE — auto handoff"
git push origin main
```

**The 5 daily principles (CAPS+G):**

| Principle | Rule |
|-----------|------|
| **C — Context first** | Load before doing. Always. |
| **A — Autonomy on details** | AI decides implementation. Human decides direction. |
| **P — Parallelism by default** | Batch tasks. Run parallel agents when available. |
| **S — Specificity** | "OVH BHS, H100, $20 max" > "affordable Canadian GPU" |
| **G — GitHub = truth** | If it's not committed, it didn't happen. |

---

## WEEKLY PROTOCOL / PROTOCOLE HEBDOMADAIRE

### [NON-DEV] The Weekly Review / La Revue Hebdomadaire

Once a week (Friday or Sunday — your choice, but consistent), run:

1. **TODO sweep**: mark completed tasks, delete irrelevant ones, add newly discovered tasks
2. **RECENT.md update**: digest the week — what was decided, what was shipped, what's at risk
3. **MetaObserver scan**: run a quick alignment check — are this week's tasks serving this month's goal?
4. **Prep next week**: identify top 3 priorities for the coming week

**Time required:** 20–30 minutes. Non-negotiable.

**Say:** *"Weekly review — update RECENT.md, sweep TODO, run MetaObserver."*

---

### [DEV] Weekly Automation

**GitHub Actions — weekly digest:**
```yaml
name: Weekly Memory Digest
on:
  schedule:
    - cron: '0 18 * * 5'  # Every Friday at 6pm

jobs:
  digest:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout memory repo
        uses: actions/checkout@v3
      
      - name: Run Archivist
        run: |
          python scripts/weekly_digest.py \
            --session-log SESSION_LOG.md \
            --output RECENT.md \
            --archive ARCHIVE/$(date +%Y-%m).md
      
      - name: Commit
        run: |
          git config user.email "archivist@enter-game"
          git config user.name "Archivist"
          git add -A
          git commit -m "weekly: $(date +%Y-%m-%d) digest"
          git push
```

**Weekly MetaObserver check (scheduled):**
```
Trigger: every Sunday, 09:00
Input: last 7 days of session logs + current CONTEXT.md + active task list
Run: all 4 monitoring modules (Direction, Role, Memory, Loop)
Output: weekly alignment report → surface to human if any Level 2+ alerts
```

---

## MONTHLY PROTOCOL / PROTOCOLE MENSUEL

### [NON-DEV] The Architecture Audit / L'Audit d'Architecture

Monthly, you zoom out. Not to execute — to check if the system is still serving you.

**Monthly checklist:**
- [ ] Memory health: is CONTEXT.md still < 60 lines? Is RECENT.md current?
- [ ] Project files: any stale projects that should be archived?
- [ ] Tool audit: is every tool in your stack still earning its cost?
- [ ] Level check: where are you on the N3→N5 scale? What's needed for the next level?
- [ ] MetaObserver full run: no alerts suppressed, all modules at full depth
- [ ] One system improvement: what's the single highest-leverage upgrade this month?

**Time required:** 1–2 hours. Do it.

---

### [DEV] Monthly Memory Maintenance

**Memory size audit:**
```bash
# Check layer sizes
wc -l CONTEXT.md RECENT.md      # L1 should be < 60 lines
ls -la projects/                 # Count active projects
du -sh ARCHIVE/                  # Monitor archive growth
```

**Stale file detection:**
```python
import os
from datetime import datetime, timedelta

STALE_THRESHOLD_DAYS = 14

for file in os.scandir('projects/'):
    mtime = datetime.fromtimestamp(file.stat().st_mtime)
    if datetime.now() - mtime > timedelta(days=STALE_THRESHOLD_DAYS):
        print(f"STALE: {file.name} — last modified {mtime.date()}")
```

**Monthly level assessment (N3→N5 check):**
```
Check N3.5 criteria:
✓ Mem0 or equivalent integrated? (Y/N)
✓ Session handoff protocol running? (Y/N)
✓ Average memory retrieval latency < 100ms? (Y/N)

Check N4 criteria:
✓ MetaObserver detecting and logging failures? (Y/N)
✓ Voice protocol formalized and reproducible? (Y/N)
✓ First RSI cycle documented? (Y/N)

If all N3.5 criteria met: you're at N3.5. Move to N4 goals.
```

---

## QUARTERLY PROTOCOL / PROTOCOLE TRIMESTRIEL

### [NON-DEV] Strategic Direction / Direction Stratégique

Quarterly, you check direction. Not "are we executing well?" but "are we executing the right things?"

**The 4 quarterly questions:**
1. What was the original plan for this quarter? What actually happened?
2. Is the current mission still the right mission? (Be honest.)
3. What's the single highest-leverage bet for next quarter?
4. What should we stop doing?

**Output:** Updated GLOBAL-PLAN reference point + updated quarterly goals in CONTEXT.md.

**Time required:** Half-day. Worth it.

---

### [DEV] Quarterly System Review

**Full pipeline audit:**
```
Agent performance review:
→ Which agent triggered the most errors this quarter?
→ Which agent had the lowest alignment score?
→ What was the most common MetaObserver alert?

Memory system review:
→ Vector DB performance: average query time, false positive rate
→ Memory layer balance: is L1 lean? Is L4 accessible?
→ Conflict resolution: how many conflicts logged?

Tool stack review:
→ Which tools were used < 5 times this quarter? (candidate for removal)
→ Which tools were bottlenecks? (candidate for upgrade)
→ New tools worth adding? (justify with specific need, not novelty)
```

---

## ANNUAL PROTOCOL / PROTOCOLE ANNUEL

### [NON-DEV] The System Upgrade / La Mise à Niveau du Système

Once a year, you're allowed to change the system. Not tweak — change. Upgrade the memory architecture. Add a new agent. Replace a tool that's been holding you back. Re-read POWERUSER.md and check if you're still at the frontier.

**Annual questions:**
1. What version of the system are you running? Is it still the best available?
2. What's one architectural assumption you made 12 months ago that's now wrong?
3. If you were starting Enter-Game from scratch today, what would you do differently?

**Output:** New system version number (e.g., v3.3 → v4.0) + changelog in DECISIONS.md.

---

### [DEV] Annual Architecture Review

**Version control for the system itself:**
```markdown
# DECISIONS.md entry — Annual review

## [YYYY-MM-DD] Annual System Upgrade — v3.3 → v4.0

### Changes
- Memory: TF-IDF → Mem0 + pgvector hybrid
- MetaObserver: added RSI capability (Module 5)
- Voice: formalized dispatch protocol (see README_voicefirst.md)

### Reasoning
- TF-IDF degraded at 300+ sessions (false positive rate ~30%)
- RSI capability available and stable enough for production
- Voice dispatch was implicit — needed documentation for Enter-Game

### Impact
- Memory retrieval accuracy: estimated +40% (pending measurement)
- Agent drift incidents: down from 8/quarter to < 2/quarter
```

---

## THE 5/10/15-YEAR FRAME / LE CADRE 5/10/15 ANS

### [NON-DEV]

This is the part most productivity systems ignore. They optimize for tomorrow. Enter-Game is built for a longer game.

**5 years:** What does the system look like when it's compounded for 5 years? What capability does that unlock? What market position?

**10 years:** What's the civilizational-scale impact if Enter-Game is adopted at scale? 10,000 solo founders operating at frontier efficiency — what does that change?

**15 years:** The protocol of equal environments. If Enter-Game succeeds at its deepest purpose, it contributes to equalizing access to high-performance operating environments across geographies, languages, and economic starting points. That's the long game.

These questions don't require action today. They require **direction**. The system is not just a productivity tool. It's a directional bet.

---

### [DEV] Linking Daily Execution to Long-Term Direction

**The connection:**
```
GLOBAL-PLAN.md  ← defines the 15-year direction
    ↓
Quarterly goals ← translate direction into 90-day execution
    ↓
Weekly priorities ← translate quarterly goals into this week's work
    ↓
Daily tasks ← what the pipeline executes today
```

**MetaObserver directional check (weekly):**
```
Input: current weekly tasks + GLOBAL-PLAN.md
Question: "Are at least 60% of active tasks traceable to the mission?"
If < 60%: surface warning
If < 40%: halt and surface to human
```

This connection — from today's task to the 15-year mission — is what distinguishes execution from drift.

---

## THE COMPLETE WORKFLOW DIAGRAM / LE DIAGRAMME COMPLET

```
┌─────────────────────────────────────────────────────────────────┐
│                         DAILY                                   │
│  context? → declare priorities → batch execute → handoff        │
└──────────────────────────┬──────────────────────────────────────┘
                           │ feeds into
┌──────────────────────────▼──────────────────────────────────────┐
│                         WEEKLY                                  │
│  TODO sweep → RECENT.md update → MetaObserver scan → prep next  │
└──────────────────────────┬──────────────────────────────────────┘
                           │ feeds into
┌──────────────────────────▼──────────────────────────────────────┐
│                         MONTHLY                                 │
│  Memory audit → level check → one system improvement           │
└──────────────────────────┬──────────────────────────────────────┘
                           │ feeds into
┌──────────────────────────▼──────────────────────────────────────┐
│                         QUARTERLY                               │
│  Direction check → stop/start/continue → update GLOBAL-PLAN ref │
└──────────────────────────┬──────────────────────────────────────┘
                           │ feeds into
┌──────────────────────────▼──────────────────────────────────────┐
│                         ANNUAL                                  │
│  System upgrade → version bump → architecture changelog         │
└──────────────────────────┬──────────────────────────────────────┘
                           │ serves
┌──────────────────────────▼──────────────────────────────────────┐
│                     5 / 10 / 15 YEARS                           │
│  GLOBAL-PLAN · civilizational direction · protocol propagation  │
└─────────────────────────────────────────────────────────────────┘
```

---

## QUICK REFERENCE / RÉFÉRENCE RAPIDE

| Frequency | Duration | Key action | Output |
|-----------|----------|------------|--------|
| Daily | 5–10 min overhead | Batch execution + handoff | Committed context |
| Weekly | 20–30 min | Review + digest | RECENT.md updated |
| Monthly | 1–2 hours | Audit + level check | Memory clean, level assessed |
| Quarterly | Half day | Direction check | GLOBAL-PLAN aligned |
| Annual | Full day | System upgrade | New version + changelog |

---

*Enter-Game · README_workflow.md · v1.0 · April 2026*
