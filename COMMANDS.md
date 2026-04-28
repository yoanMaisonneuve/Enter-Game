# COMMANDS.md
## The Enter-Game Agentic Layer / La Couche Agentique Enter-Game

**Enter-Game · v1.1 · April 2026**

---

> This is not documentation. This is the operating protocol.
> Say the command. Get the output. Move.
>
> *Ce n'est pas de la documentation. C'est le protocole opératoire.
> Dis la commande. Obtiens l'output. Avance.*

---

## HOW TO USE / COMMENT UTILISER

These commands work in any Claude session where your CLAUDE.md is loaded.
Speak them out loud (voice-first) or type them directly.
Claude executes and returns the output. No explanation needed.

*Ces commandes fonctionnent dans toute session Claude où ton CLAUDE.md est chargé.
Dis-les à voix haute (voice-first) ou tape-les directement.
Claude exécute et retourne l'output. Pas d'explication nécessaire.*

---

## TIER 1 — CORE SESSION (every session / chaque session)

| Command | What happens | Output |
|---------|-------------|--------|
| `contexte` | Load current state from CONTEXT.md + RECENT.md | Active state summary |
| `go [tâche]` | Execute task immediately, no preamble | Task output |
| `handoff` | Archive session: log decisions, update RECENT.md, commit to GitHub | Commit confirmation |
| `status` | Project health check: what's done, in progress, blocked | Status report |

**Session pattern:**
```
contexte → declare 1–3 priorities → go [batch tasks] → handoff
```

---

## TIER 2 — CAPTURE (voice-first / mobile)

| Command | What happens | Output |
|---------|-------------|--------|
| `idée [texte]` | Structure idea + push to GitHub via enter-game hub | .md committed to repo |
| `note [texte]` | Raw capture, no structure, push immediately | .md committed |
| `interview-moi sur [X]` | 5–8 pre-decision questions on blind spots | Q&A + decision clarity |
| `décide [X]` | Decision framework: options, trade-offs, recommendation | Decision doc |

**Voice trigger:**
```
"idée: je veux ajouter une couche mémoire vectorielle à Blueprint"
→ Claude structures it → pushes to GitHub → confirms
```

---

## TIER 3 — BUILD (most used daily tasks / tâches quotidiennes les plus utilisées)

| Command | What happens | Output |
|---------|-------------|--------|
| `spec [sujet]` | Write PRD/feature spec with goals, scope, success metrics | Spec Markdown |
| `docs [sujet]` | Write technical documentation | Doc Markdown |
| `revue [code/fichier/PR]` | Code review: security, performance, correctness | Review report |
| `debug [problème]` | Structured debug session: reproduce → isolate → fix | Fix + explanation |
| `test [composant]` | Test strategy for a component or system | Test plan |
| `architecture [problème]` | ADR: options, trade-offs, recommendation | Architecture decision |

**Build batch example:**
```
go: spec API auth + docs onboarding + revue auth.py
→ Claude produces all three in one pass
```

---

## TIER 4 — PLAN (weekly / weekly)

| Command | What happens | Output |
|---------|-------------|--------|
| `standup` | Generate daily update from recent activity | Standup (yesterday / today / blockers) |
| `plan [semaine/sprint]` | Sprint planning: scope, capacity, priorities | Sprint plan |
| `tâches` | Show and update task list | TASKS.md rendered |
| `roadmap [horizon]` | Update or create roadmap for given horizon | Roadmap Markdown |
| `risques [projet/décision]` | Risk assessment + mitigation | Risk register |

---

## TIER 5 — MEMORY (session hygiene / hygiène de session)

| Command | What happens | Output |
|---------|-------------|--------|
| `mémoire [X]` | Save fact/decision/context to memory files | Memory file updated |
| `oublie [X]` | Remove stale memory entry | Memory file updated |
| `archive` | Move completed project context to ARCHIVE/ | Archive commit |
| `rappel` | Show what memory has loaded in current session | Memory summary |

---

## TIER 6 — OUTPUT (artefacts / deliverables)

| Command | What happens | Output |
|---------|-------------|--------|
| `rapport [sujet]` | Write synthesis report on a topic | Report .md |
| `email [destinataire / sujet]` | Draft email with appropriate tone | Email draft |
| `présentation [sujet]` | Slide deck outline or full .pptx | Presentation |
| `tableau [données]` | Data table or spreadsheet | .xlsx or Markdown table |

---

## TIER 7 — AGENT PIPELINE (advanced / avancé)

| Command | What happens | Output |
|---------|-------------|--------|
| `pipeline [objectif]` | Activate full 7-agent sequence: Planner → Researcher → Analyst → Builder → Reviewer → Archivist | Full deliverable |
| `planner [objectif]` | Decompose objective into ordered tasks | Task breakdown |
| `recherche [sujet]` | Deep research on a topic | Structured findings |
| `métaobs` | Run MetaObserver scan: direction, coherence, drift | System health report |

---

## COMMAND COMBINATIONS / COMBINAISONS

### Morning session (5 min setup)
```
contexte
→ standup
→ plan aujourd'hui: [priorité 1] + [priorité 2] + [priorité 3]
```

### Build session
```
contexte
→ interview-moi sur [la feature qu'on va construire]
→ go: spec [feature] + architecture [décision clé]
→ handoff
```

### Capture session (mobile, voice-first)
```
idée: [brut, non-structuré]
→ Claude structure + push
→ continuer à marcher
```

### End of week
```
status
→ archive [projets complétés]
→ plan semaine prochaine
→ handoff
```

---

## RULES / RÈGLES

1. **Batch > séquentiel** — 3 tâches dans un prompt > 3 prompts séparés
2. **Pas de session sans handoff** — si tu fermes sans handoff, le contexte est perdu
3. **Interview avant architecture** — toute décision structurelle non-triviale mérite 5 questions
4. **go = exécution immédiate** — pas d'explication, pas de plan affiché, juste l'output
5. **idée = capture sans friction** — même brute, même incomplète, capture d'abord, structure après

---

## SKILL MAPPING (Cowork)

Commands map to Cowork skills automatically when available:

| Command | Cowork Skill |
|---------|-------------|
| `spec` | product-management:write-spec |
| `standup` | engineering:standup |
| `plan sprint` | product-management:sprint-planning |
| `status` | operations:status-report |
| `revue` | engineering:code-review |
| `debug` | engineering:debug |
| `docs` | engineering:documentation |
| `architecture` | engineering:architecture |
| `risques` | operations:risk-assessment |
| `tâches` | productivity:task-management |
| `mémoire` | productivity:memory-management |
| `rapport` | operations:status-report |
| `présentation` | pptx |
| `tableau` | xlsx |
| `interview-moi` | (built-in — no skill needed) |

---

*Enter-Game · v1.1 · "You don't start a company. You enter the game."*
