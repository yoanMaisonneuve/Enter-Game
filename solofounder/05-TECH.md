# 05 — TECH / PRODUCTION
## Code · Architecture · Infra · Deploy · QA

**Enter-Game Solofounder · April 2026**

> As solo founder, you're the CTO.
> You don't need to be the best engineer in the room.
> You need to ship, maintain, and not break things in production.

---

> See also: `../skills/04-CODE.md` for complete engineering commands.
> This file covers the CTO decision layer — what to build, how to build it, when to stop.

---

## SKILLS / COMPÉTENCES

---

### TECH-DECISION — Make a technology decision

**Command:**
```
tech-decision: [choice to make: framework / database / service / architecture] · [constraints: team size = 1, budget, scale expectations] · [options you're considering]
```
**Output:** Decision with: comparison, recommendation for solo founder context, risks, reversibility score.

---

### MVP-STACK — Choose your MVP stack

**Command:**
```
mvp-stack: [what you're building: type of product] · [your current skills] · [target: ship in X weeks] · [scale expectations]
```
**Output:** Recommended stack for a solo founder to ship fastest. Reasoning. Common mistakes to avoid.

---

### TECH-DEBT — Assess technical debt

**Command:**
```
tech-debt: [describe current codebase or architecture] · [what's slowing you down] · [what's scary to touch]
```
**Output:** Tech debt register with: severity, impact on velocity, recommended order to address, what to tolerate for now.

---

### ARCHITECTURE — System architecture

**Command:**
```
architecture: [what the system needs to do] · [current state] · [scale: users, data, throughput] · [constraints: cost, solo maintainability]
```
**Output:** Architecture recommendation optimized for solo maintainability + cost + good enough for scale.

---

### INFRA-COST — Estimate infrastructure costs

**Command:**
```
infra-cost: [stack: what services you're using or planning] · [scale: users / requests / data] · [provider: AWS / GCP / Azure / Vercel / Supabase]
```
**Output:** Monthly cost estimate at current scale + at 10x + at 100x. Optimization suggestions.

---

### SECURITY-BASELINE — Security baseline for solo founder

**Command:**
```
security-baseline: [type of product: SaaS / API / consumer app] · [what data you handle] · [current state]
```
**Output:** Minimum security checklist for a solo founder — what you must have vs what can wait. Prioritized.

---

## QUICK REFERENCE

```
tech-decision      → framework / database / architecture choice
mvp-stack          → fastest stack to ship for solo founder
tech-debt          → technical debt assessment
architecture       → system design
infra-cost         → cost estimation by scale
security-baseline  → minimum security checklist
```

→ For code-level skills (revue, debug, tests, docs): see `../skills/04-CODE.md`

---

*Enter-Game Solofounder · 05-TECH · v1.1*
