# README_agents.md
## The 7-Agent Pipeline / Le Pipeline 7 Agents

**Enter-Game · v1.0 · April 2026**

---

> This document teaches the 7-agent pipeline that powers the Enter-Game protocol.
> Someone who forks this repo should be able to reconstruct the full system from this README alone.
>
> *Ce document enseigne le pipeline 7 agents qui propulse le protocole Enter-Game.
> Quelqu'un qui fork ce repo doit pouvoir reconstruire le système complet depuis ce README seul.*

---

## TWO READING MODES / DEUX MODES DE LECTURE

| 🛠️ **DEV BRANCH** | 🧭 **NON-DEV BRANCH** |
|---|---|
| Technical architecture, orchestration patterns, prompt specs, parallelism | Plain language, human analogies, operational workflow without code |
| Look for `[DEV]` markers | Look for `[NON-DEV]` markers |

---

## THE PIPELINE / LE PIPELINE

```
                    ┌─────────────────────────────────────────┐
                    │         MetaObserver (Layer 7)          │
                    │   Watches everything · Corrects drift   │
                    └─────────────────────────────────────────┘
                                        │
         ┌──────────────────────────────┼──────────────────────────────┐
         ▼              ▼              ▼              ▼               ▼
    [1] Planner  [2] Researcher  [3] Analyst  [4] Builder  [5] Reviewer
         │                                         │
         └──────────────────[6] Archivist──────────┘
                         (runs after any agent)
```

**Sequential mode (default):**
```
Planner → Researcher → Analyst → Builder → Reviewer → Archivist
```

**Parallel mode (advanced):**
```
Planner → [Researcher A + Researcher B in parallel] → Analyst → Builder → Reviewer → Archivist
```

---

## AGENT 1 — PLANNER

### [NON-DEV] The Strategist / Le Stratège

The Planner is the first agent you activate. Before anything is built or researched, the Planner decomposes your objective into a structured task sequence. Think of it as the project manager who asks "what exactly needs to happen, in what order, with what constraints?" before the team starts.

**When to activate:** Every time you have a non-trivial goal. If you can execute a task in one step, you don't need the Planner. If it takes more than 3 steps, always start here.

**What you give it:** Your objective, constraints, available context.

**What you get back:** A prioritized task list, success criteria, flags on risks.

---

### [DEV] Technical Spec

**Role:** Task decomposition + sequencing + dependency mapping

**Inputs:**
- Objective (free text or structured)
- Available context (CONTEXT.md, project files)
- Constraints (time, budget, tools)

**Outputs:**
- Ordered task list (JSON or markdown)
- Inter-task dependencies
- Confidence score per task
- Escalation triggers (when to stop and ask the human)

**Activation pattern (n8n / LangGraph):**
```
trigger: new_task_request
→ load_context(CONTEXT.md, RECENT.md, project.md)
→ call_planner_agent(system_prompt=PLANNER_PROMPT, input=task_request)
→ output: structured_plan.json
→ route: if plan.requires_research → Researcher | else → Builder
```

**System prompt skeleton:**
```
You are the Planner agent in the Enter-Game pipeline.
Your role is to decompose a complex objective into an ordered, executable task sequence.

Rules:
- Always identify dependencies before sequencing tasks
- Flag tasks requiring human validation (budget > $X, production deployments, irreversible actions)
- Output format: JSON with fields: tasks[], dependencies{}, risks[], escalation_triggers[]
- Never execute tasks yourself — you plan, others execute
- If context is insufficient, output: {status: "needs_context", missing: [...]}
```

---

## AGENT 2 — RESEARCHER

### [NON-DEV] The Scout / L'Éclaireur

The Researcher goes out and collects information before anything is built. It searches the web, reads documentation, queries databases, and retrieves relevant memory. It's the agent that makes sure the Builder has everything it needs before starting — no building on wrong assumptions.

**When to activate:** Whenever the task requires external information, documentation lookup, competitive research, or context that isn't already loaded.

**What you give it:** A research brief (what to find, from where, at what depth).

**What you get back:** Structured findings, source references, confidence level per finding.

---

### [DEV] Technical Spec

**Role:** Context retrieval + external search + memory query

**Inputs:**
- Research brief from Planner
- Memory layer access (L1–L4)
- Tool access: web search, file system, APIs, vector DB

**Outputs:**
- Structured research report (markdown)
- Source citations
- Confidence scores
- Gaps flagged (what couldn't be found)

**Tools to connect:**
```
- Web search (Brave/Perplexity API)
- Vector DB query (pgvector / Mem0)
- GitHub file reader
- API connectors (Stripe, Supabase, etc.)
- Web scraper (for documentation)
```

**Activation pattern:**
```
input: research_brief.json (from Planner)
→ parallel_search([web_query, memory_query, docs_query])
→ deduplicate_and_rank(results)
→ output: research_report.md
→ confidence_gate: if avg_confidence < 0.6 → flag_for_human_review
```

---

## AGENT 3 — ANALYST

### [NON-DEV] The Filter / Le Filtre

The Analyst processes what the Researcher found. Raw information is noise — the Analyst extracts signal. It ranks, connects, and synthesizes findings into actionable insights. It answers: "Given everything we found, what actually matters for what we're trying to do?"

**When to activate:** Always after the Researcher, before the Builder. Skipping the Analyst is the most common reason pipelines produce irrelevant outputs.

**What you give it:** The raw research report.

**What you get back:** Ranked insights, recommended direction, risks identified.

---

### [DEV] Technical Spec

**Role:** Information processing, synthesis, prioritization, risk identification

**Inputs:**
- Research report from Researcher
- Task brief from Planner (as alignment reference)
- Historical decisions (DECISIONS.md) for conflict checking

**Outputs:**
- Insight ranking (impact × confidence × novelty)
- Recommended direction (with reasoning)
- Risk matrix (probability × impact)
- Contradictions with existing decisions flagged

**Analytical frameworks applied by default:**
```
1. Signal/noise separation: filter findings below confidence threshold
2. Alignment check: does finding change the Planner's task sequence?
3. Risk scoring: assign P(risk) × Impact for each risk identified
4. Decision conflict: cross-check against DECISIONS.md
```

**Output format:**
```json
{
  "insights": [
    {"finding": "...", "impact": "high", "confidence": 0.85, "action": "..."}
  ],
  "recommended_direction": "...",
  "risks": [
    {"description": "...", "probability": 0.3, "impact": "high", "mitigation": "..."}
  ],
  "conflicts_with_decisions": []
}
```

---

## AGENT 4 — BUILDER

### [NON-DEV] The Executor / L'Exécuteur

The Builder is where things get made. Code, content, configurations, documents — the Builder executes. It is the highest-output agent in the pipeline. It works from a precise brief (Planner + Analyst combined) and builds without asking unnecessary questions.

**When to activate:** When you have a clear brief, necessary context, and resolved risks. If any of those three are missing, go back to Analyst.

**What you give it:** The execution brief (what to build, specs, constraints, acceptance criteria).

**What you get back:** The deliverable — code, content, configuration, or document.

---

### [DEV] Technical Spec

**Role:** Code generation, content creation, system configuration, deployment scripting

**Inputs:**
- Execution brief (from Planner + Analyst synthesis)
- Technical constraints (language, framework, infra target)
- Memory access: code templates, prior implementations

**Outputs:**
- Deliverable (code files, content, configs)
- Implementation notes
- Test suggestions
- Next step recommendations

**Specialization variants:**
```
Builder-Code:     generates and refactors code, writes tests
Builder-Content:  writes documentation, copy, reports
Builder-Config:   generates Kubernetes, Docker, CI/CD files
Builder-Script:   automation scripts, data processing
```

**Gate before execution:**
```
Pre-flight check:
✓ Has complete execution brief?
✓ All dependencies resolved?
✓ No unresolved conflicts from Analyst?
✓ Human validation required? (production deploy, budget > threshold)
→ If all pass: execute
→ If any fail: route back to appropriate prior agent
```

---

## AGENT 5 — REVIEWER

### [NON-DEV] The Quality Gate / La Porte Qualité

The Reviewer is the last checkpoint before output is accepted. It checks: does the deliverable match the original brief? Are there errors, gaps, or misalignments? Does this introduce new risks? The Reviewer is not the Builder critiquing itself — it's a separate pass with a different lens.

**When to activate:** After every Builder output, before the Archivist saves anything.

**What you give it:** The deliverable + the original brief.

**What you get back:** Pass/fail verdict, specific issues if any, severity scoring.

---

### [DEV] Technical Spec

**Role:** Quality assurance, alignment verification, risk re-assessment

**Inputs:**
- Builder output (deliverable)
- Original task brief (from Planner)
- Acceptance criteria
- Risk matrix (from Analyst)

**Outputs:**
- Review verdict: PASS | PASS_WITH_NOTES | FAIL
- Issue list (severity: critical / major / minor)
- Alignment score (0–100, deliverable vs brief)
- Recommendations if FAIL

**Review dimensions:**
```
1. Correctness:     does it work / does it do what was asked?
2. Completeness:    are all requirements addressed?
3. Consistency:     no contradictions with existing decisions/code?
4. Risk:            does it introduce new risks not in the risk matrix?
5. Standard:        follows project conventions and quality standards?
```

**Routing logic:**
```
if verdict == PASS → Archivist
if verdict == PASS_WITH_NOTES → Archivist + flag_for_human_review
if verdict == FAIL → route_back_to_builder(with_issues)
if verdict == FAIL (2nd time) → route_to_human + pause_pipeline
```

---

## AGENT 6 — ARCHIVIST

### [NON-DEV] The Memory Keeper / Le Gardien de la Mémoire

The Archivist runs after every significant output. Its job: decide what to keep, where to store it, and what to remove. It maintains the health of the memory system. Without the Archivist, the system accumulates noise until context quality degrades.

**When to activate:** After Reviewer passes output. Also: at session end (handoff protocol).

**What you give it:** The approved deliverable + metadata.

**What you get back:** Updated memory files, archive entry, session handoff summary.

---

### [DEV] Technical Spec

**Role:** Memory management, context update, session handoff, archival

**Inputs:**
- Reviewed deliverable + metadata
- Current memory state (CONTEXT.md, RECENT.md, projects/)
- Session log (all decisions made this session)

**Outputs:**
- Updated CONTEXT.md (if relevant facts changed)
- Updated RECENT.md (session digest)
- Archive entry (ARCHIVE/YYYY-MM.md)
- Updated project file (projects/[project].md)
- DECISIONS.md entry if major decision was made

**Decision rules for memory operations:**
```
PROMOTE to L1 (CONTEXT.md):  locked decisions, critical constraints, role definitions
KEEP in L2 (RECENT.md):      last 2–4 weeks of active context
DEMOTE to L3 (projects/):    project-specific context no longer in active session
ARCHIVE to L4:                completed projects, old decisions, resolved issues
DISCARD:                      drafts superseded by final version, temporary notes
```

**Session handoff template:**
```markdown
## Session [YYYY-MM-DD] Handoff
- Tasks completed: [list]
- Decisions made: [list with reasoning]
- Memory updates: [what was promoted/demoted/archived]
- Active risks: [carry-forward risks]
- Next session priority: [top 1–2 actions]
```

---

## AGENT 7 — METAOBSERVER

### [NON-DEV] The System Watcher / Le Gardien du Système

The MetaObserver is not an execution agent. It sits above the pipeline and watches the whole system. It answers one question: "Is everything aligned with where we decided to go?" It fires when drift is detected — when tasks stop serving the mission, when agents loop, when memory degrades, when the system starts optimizing the wrong things.

Most systems don't have this layer. That's why most systems drift.

**When it activates:** On a schedule (e.g., weekly), at session end, or when triggered by anomaly detection in other agents.

**What you give it:** The full system state — active tasks, recent decisions, current direction, memory health.

**What you get back:** Alignment score, drift report, corrective recommendations.

---

### [DEV] Technical Spec

**Role:** Metacognitive monitoring, drift detection, system governance

**4 Monitoring Modules:**

```
Module 1 — DIRECTIONAL MONITOR
  Input: active task list + GLOBAL-PLAN / mission statement
  Check: are current tasks advancing the stated mission?
  Alert threshold: < 60% of tasks aligned with mission
  Output: alignment score + list of off-mission tasks

Module 2 — ROLE MONITOR
  Input: agent execution logs
  Check: is each agent executing its designated function?
  Alert: Builder doing Analyst work? Researcher making architectural decisions?
  Output: role deviation report

Module 3 — MEMORY MONITOR
  Input: CONTEXT.md + RECENT.md + memory freshness timestamps
  Check: is critical context accessible, non-corrupted, non-stale?
  Alert threshold: any L1 file > 14 days without review
  Output: memory health report + stale files flagged

Module 4 — LOOP DETECTOR
  Input: task history (last 7 days)
  Check: are we executing the same task category repeatedly without progress?
  Alert threshold: same task type > 3 times without state change
  Output: loop alert + break-loop recommendation
```

**Intervention levels:**
```
Level 1 (Advisory):    log anomaly, add to next session briefing
Level 2 (Warning):     interrupt current pipeline, surface to human
Level 3 (Emergency):   halt pipeline, require human validation to resume
```

**Self-improvement capability (frontier — N4+):**
```
If same failure pattern detected > 2 times:
→ generate updated monitoring rule
→ stage rule for human review
→ if approved: update monitoring module
→ log rule change in DECISIONS.md
```

---

## ACTIVATION GUIDE / GUIDE D'ACTIVATION

### When to use which agent / Quand activer quel agent

| Situation | Agents to activate |
|-----------|-------------------|
| New project, fuzzy objective | Planner → Interview Rule → Planner (revised) |
| Research-heavy task | Researcher → Analyst → Builder |
| Pure execution (clear spec) | Builder → Reviewer → Archivist |
| Session end | Archivist → MetaObserver (brief) |
| Weekly review | MetaObserver (full run) |
| Major decision | Interview Rule + Planner + Analyst + MetaObserver check |
| Pipeline feels stuck | MetaObserver → Loop Detector |

---

### [DEV] Orchestration Setup / Setup d'Orchestration

**Minimal setup (Claude Projects / single AI):**
```
Each "agent" = a different system prompt loaded for that phase.
Use explicit handoffs: "ARCHIVIST MODE: [input]" or "METAOBSERVER MODE: run weekly check"
All agents read from the same memory files (CONTEXT.md, etc.)
```

**Advanced setup (n8n + MCP):**
```
Each agent = a dedicated n8n workflow node
MetaObserver = scheduled trigger (weekly) + webhook trigger (anomaly)
Each agent outputs structured JSON consumed by the next
Archivist = GitHub API writes to memory repo after every significant output
```

**LangGraph pattern:**
```python
workflow = StateGraph(PipelineState)
workflow.add_node("planner", planner_agent)
workflow.add_node("researcher", researcher_agent)
workflow.add_node("analyst", analyst_agent)
workflow.add_node("builder", builder_agent)
workflow.add_node("reviewer", reviewer_agent)
workflow.add_node("archivist", archivist_agent)
# MetaObserver runs as a separate process / scheduled job
workflow.add_conditional_edges("reviewer", route_after_review)
```

---

## THE HUMAN ROLE / LE RÔLE HUMAIN

The pipeline doesn't replace the human. It amplifies the human.

**You decide:**
- The mission and direction
- Major architectural choices
- Production deployments
- Budget authorization
- What to build next

**The pipeline executes:**
- Research
- Analysis
- Code and content
- Quality checking
- Memory management
- System monitoring

The rule: **strategic decisions stay with the human. Execution delegates to the pipeline.**

---

*Enter-Game · README_agents.md · v1.0 · April 2026*
