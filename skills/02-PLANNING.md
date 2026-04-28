# 02 — PLANNING
## Status · Tasks · Roadmap · Standup · Sprint

**Enter-Game Skills · April 2026**

> Status-chasing, update writing, and priority-setting consume
> 20–30% of manager time. This domain reclaims it.

---

## USAGE RANK: #2 for managers and team leads

Critical for: founders, project managers, team leads, product managers, ops leads.
Impact: less time on reporting, more time on decisions.

---

## SKILLS / COMPÉTENCES

---

### STATUS — Generate a project status report

**Command:**
```
status: [project name] · [what's done] · [in progress] · [blocked] · [audience: team / management / exec]
```

**Output:** Formatted status report with RAG indicator (Red/Amber/Green), summary, risks, next actions.

**Template:**
```
status:
Project: [name]
Done this week: [bullet list]
In progress: [bullet list]
Blocked: [what + who unblocks it]
Next week: [priorities]
Audience: [team / management / exec]
```

---

### STANDUP — Daily standup update

**Command:**
```
standup: [yesterday] · [today] · [blockers]
```

**Output:** Formatted standup for team channel (Slack, Teams, or async). Concise, scannable.

**Example:**
```
standup: finished auth API · integrating payment SDK today · waiting on design specs for checkout page
```

---

### TASKS — Show and manage task list

**Command:**
```
tâches
```
or
```
tasks: [add/complete/prioritize] · [task description]
```

**Output:**
- Current task list with priorities
- Suggested next action based on urgency/importance
- Flagged items: overdue, blocked, deprioritized

---

### PRIORITIZE — Prioritize a list of tasks or projects

**Command:**
```
prioritize: [paste list of tasks or projects] · [criteria: impact / urgency / effort / dependencies]
```

**Output:** Prioritized list with reasoning. Uses impact/effort matrix when no criteria specified.

---

### SPRINT-PLAN — Plan a sprint or work week

**Command:**
```
sprint-plan: [team size] · [capacity: hours or days] · [backlog items] · [goal for this sprint]
```

**Output:** Sprint plan with scope, allocation per person, acceptance criteria, buffer for unplanned work.

---

### ROADMAP — Create or update a roadmap

**Command:**
```
roadmap: [product/project name] · [horizon: Q / 6mo / 1yr] · [known initiatives] · [constraints]
```

**Output:** Roadmap in Now/Next/Later format (or quarterly if specified). With rationale for prioritization.

---

### OKR — Write OKRs

**Command:**
```
okr: [team/company] · [time period] · [strategic direction or problem to solve]
```

**Output:** 2–4 Objectives with 3 Key Results each. Measurable, time-bound, ambitious but achievable.

---

### RETROSPECTIVE — Run a retrospective

**Command:**
```
retro: [project or sprint] · [what went well] · [what didn't] · [team size]
```

**Output:** Structured retrospective with themes, root causes, and 3–5 actionable improvements.

---

### RISK-REGISTER — Identify and assess risks

**Command:**
```
risques: [project or initiative] · [context: scope, timeline, team, dependencies]
```

**Output:** Risk register with probability, impact, mitigation per risk. Top 3 highlighted.

---

### DECISION-LOG — Document a decision

**Command:**
```
décision: [what was decided] · [why] · [alternatives considered] · [who decided] · [date]
```

**Output:** Decision record in ADR format. Ready to commit to repo or add to project doc.

---

### WEEKLY-REVIEW — Weekly review and planning

**Command:**
```
weekly-review: [what happened this week] · [what didn't get done] · [priorities for next week]
```

**Output:** Structured weekly review with wins, misses (no judgment), carryover, and next-week plan.

---

## QUICK REFERENCE / RÉFÉRENCE RAPIDE

```
status          → project status report (RAG)
standup         → daily async update
tâches          → task list management
prioritize      → rank tasks by impact/effort
sprint-plan     → weekly or sprint planning
roadmap         → Now/Next/Later roadmap
okr             → OKR writing
retro           → retrospective
risques         → risk register
décision        → decision record
weekly-review   → end-of-week review
```

---

## TIME SAVED

| Task | Before AI | With AI | Saving |
|------|-----------|---------|--------|
| Status report | 45–60 min | 5–10 min | ~85% |
| Sprint planning | 3–4 hours | 45–90 min | ~70% |
| Risk register | 2–3 hours | 20–30 min | ~80% |
| Weekly review | 30–45 min | 10 min | ~70% |
| OKR writing | 2–4 hours | 30–60 min | ~75% |

---

*Enter-Game Skills · 02-PLANNING · v1.1*
