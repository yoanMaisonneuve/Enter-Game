# 04 — CODE
## Development · Review · Debug · Documentation · Testing

**Enter-Game Skills · April 2026**

> Software engineering = ~50% of all Claude API traffic (Anthropic Economic Index, Jan 2026).
> 80% of tech leaders reported using AI in software development in 2025.
> This domain has the highest absolute volume of AI usage across all industries.

---

## USAGE RANK: #1 for engineers, #1 by API volume overall

Critical for: software engineers, architects, DevOps, tech leads, CTOs, full-stack founders.

---

## SKILLS / COMPÉTENCES

---

### CODE-REVIEW — Review code

**Command:**
```
revue: [paste code or PR diff] · [focus: security / performance / correctness / all]
```

**Output:** Review report with:
- Issues ranked by severity (critical / major / minor)
- Specific line-level feedback
- Security flags highlighted separately
- Suggested fixes for top issues

---

### DEBUG — Debug a problem

**Command:**
```
debug: [describe problem] · [paste error message or stack trace] · [context: language, framework, what changed]
```

**Output:** Structured debug session:
1. Most likely root causes (ranked)
2. How to reproduce and isolate
3. Proposed fix with code
4. How to verify the fix worked

---

### SPEC-TECH — Write a technical spec

**Command:**
```
spec-tech: [feature or system to specify] · [constraints: tech stack, scale, existing architecture] · [audience: dev team]
```

**Output:** Technical spec with: problem statement, proposed solution, architecture diagram (text), API contracts, edge cases, open questions.

---

### ARCHITECTURE — Architecture decision

**Command:**
```
architecture: [problem to solve] · [options considered] · [constraints: performance, cost, team skills] · [context]
```

**Output:** ADR (Architecture Decision Record):
- Context and problem
- Options considered with pros/cons
- Decision with rationale
- Consequences (trade-offs accepted)

---

### CODE-DOCS — Document code

**Command:**
```
code-docs: [paste code] · [type: README / inline comments / API reference / runbook]
```

**Output:** Documentation in the requested format. Inline comments explain non-obvious logic. READMEs include setup, usage, and examples.

---

### TEST — Write tests or test strategy

**Command:**
```
test: [component or function] · [type: unit / integration / e2e / all] · [framework if specified]
```

**Output:**
- Test cases covering happy path, edge cases, error states
- Code for specified framework
- Coverage gaps flagged

---

### REFACTOR — Refactor code

**Command:**
```
refactor: [paste code] · [goal: readability / performance / DRY / SOLID / all]
```

**Output:** Refactored code with explanation of each change. Original preserved for comparison.

---

### SQL — Write or optimize SQL

**Command:**
```
sql: [what you want to query] · [schema: paste table definitions] · [database: PostgreSQL / MySQL / etc.]
```

**Output:** SQL query, optimized if possible. Index suggestions if applicable.

---

### DEPLOY — Deployment checklist

**Command:**
```
déploie: [what's being deployed] · [environment: staging / prod] · [changes included] · [rollback plan]
```

**Output:** Pre-deployment checklist with verification steps, rollback triggers, and post-deployment validation.

---

### INCIDENT — Incident response

**Command:**
```
incident: [what broke] · [symptoms observed] · [impact: users affected, services down] · [what's been tried]
```

**Output:**
- Triage assessment (severity)
- Immediate actions to stabilize
- Investigation steps
- Communication template for stakeholders
- Post-mortem template

---

### POSTMORTEM — Write a post-mortem

**Command:**
```
postmortem: [incident summary] · [timeline] · [root cause] · [impact] · [what was done]
```

**Output:** Blameless post-mortem with timeline, root cause analysis, contributing factors, action items to prevent recurrence.

---

### README — Write a README

**Command:**
```
readme: [project name] · [what it does] · [tech stack] · [key features] · [target audience: devs / users]
```

**Output:** Complete README with: description, features, installation, usage, configuration, contributing, license.

---

### SECURITY — Security review

**Command:**
```
security-review: [paste code or architecture] · [threat model: what are you protecting against]
```

**Output:** Security review with:
- Vulnerabilities found (OWASP classification)
- Severity per finding
- Remediation recommendations
- What was not checked (scope limitations)

---

## QUICK REFERENCE / RÉFÉRENCE RAPIDE

```
revue          → code review (security, perf, correctness)
debug          → structured debug session
spec-tech      → technical specification
architecture   → architecture decision record
code-docs      → document code / write README
test           → write tests or test strategy
refactor       → refactor for readability / performance
sql            → write or optimize SQL
déploie        → deployment checklist
incident       → incident response
postmortem     → post-mortem document
readme         → project README
security-review → security audit
```

---

## THE DEVELOPER FLYWHEEL

The compounding effect for engineering teams:
1. `revue` catches bugs before production → fewer `debug` sessions → fewer `incident` responses
2. `code-docs` + `readme` → faster onboarding → faster new contributor velocity
3. `test` → higher coverage → more confident refactoring
4. `postmortem` → documented learnings → the same failure doesn't happen twice

One team that systematically uses these 4 skills (`revue` + `code-docs` + `test` + `postmortem`) compounds quality over time. Technical debt decreases. Velocity increases.

---

*Enter-Game Skills · 04-CODE · v1.1*
