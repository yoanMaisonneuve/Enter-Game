# 02 — VENTES
## Lead Gen · Prospecting · Demos · Closing · CRM · Suivi

**Enter-Game Solofounder · April 2026**

> The solo founder's #1 mistake: building without selling.
> The CEO function is the meta-layer above everything else.
> Sales is the proof that what you built matters.
> No pipeline = no company.

---

## SKILLS / COMPÉTENCES

---

## SECTION A — LEAD GENERATION / GÉNÉRATION DE LEADS

---

### LEAD-SCAN — Scan leads by industry sector

**Command:**
```
lead-scan: [your offer: what you sell] · [secteur cible: list 1–3 industries] · [ideal company size] · [géographie] · [trigger events to look for]
```

**Output:**
- 10–20 lead profiles matching criteria (company type, role to target, why they'd buy now)
- Trigger events that signal buying intent per sector
- Recommended channels to find them (LinkedIn, industry associations, conferences, subreddits)
- Prioritized outreach order

**Example:**
```
lead-scan: outil IA pour gestion de projet · secteurs: construction / manufacturing / logistique · PME 50–500 employés · Canada + France · trigger: levée de fonds récente, croissance rapide, nouveau DG
```

---

### LEAD-SCAN-SECTOR — Deep scan by specific sector

Pre-built sector scans. Copy the command, fill in your offer:

**Construction / BTP:**
```
lead-scan-sector: construction · [votre offre] · cibles: directeurs de projet, VP Ops, CTO · triggers: appels d'offres publics, nouveaux chantiers, conformité réglementaire
```

**Manufacturing / Industrie:**
```
lead-scan-sector: manufacturing · [votre offre] · cibles: VP Opérations, directeur production, DG · triggers: expansion capacité, problèmes qualité, réduction coûts
```

**Logistique / Supply Chain:**
```
lead-scan-sector: logistique · [votre offre] · cibles: directeur supply chain, VP logistique · triggers: croissance volumes, nouvelles routes, problèmes livraison
```

**Finance / Comptabilité:**
```
lead-scan-sector: finance · [votre offre] · cibles: CFO, directeur financier, DAF · triggers: croissance PME, audit externe, nouvelles normes comptables
```

**Santé / Healthcare:**
```
lead-scan-sector: santé · [votre offre] · cibles: directeur clinique, gestionnaire d'hôpital, DSI · triggers: transformation numérique, normes MSSS, expansion
```

**Retail / Commerce:**
```
lead-scan-sector: retail · [votre offre] · cibles: directeur marketing, VP ecommerce, CMO · triggers: saison haute, lancement produit, concurrence accrue
```

**Tech / SaaS:**
```
lead-scan-sector: tech · [votre offre] · cibles: CTO, VP Engineering, Head of Product · triggers: levée de fonds, scaling équipe, dette technique, lancement
```

**Éducation / Formation:**
```
lead-scan-sector: éducation · [votre offre] · cibles: directeur pédagogique, DRH, responsable formation · triggers: rentrée, réforme, budget Q1/Q4
```

---

### ICP — Define Ideal Customer Profile

**Command:**
```
icp: [your product / offer] · [customers who've gotten value: describe] · [deals that closed fast] · [deals that didn't work]
```

**Output:** ICP definition with:
- Firmographic criteria (size, industry, geography, revenue)
- Technographic fit (what tools they use)
- Psychographic fit (how they think, what they value)
- Trigger events that create urgency
- Anti-ICP (who to avoid)

---

### PROSPECT-RESEARCH — Research a specific prospect

**Command:**
```
prospect: [company name] · [your offer] · [what you know about them]
```

**Output:**
- Company overview (industry, size, likely challenges)
- Decision-maker profile (role, likely pain points)
- Relevant trigger events
- Personalized outreach angle
- Opening question to lead with

---

## SECTION B — OUTREACH / PROSPECTION

---

### COLD-EMAIL — Write cold email

**Command:**
```
cold-email: [prospect: role + company + context] · [your offer in 1 line] · [angle: pain / opportunity / referral / trigger event]
```

**Output:** Cold email under 100 words. Subject line + body + CTA (one question, not a pitch).

---

### LINKEDIN-OUTREACH — Write LinkedIn outreach

**Command:**
```
linkedin: [prospect name / role] · [connection angle] · [your offer] · [one reason why now]
```

**Output:** LinkedIn connection request note (< 300 chars) OR InMail (< 400 chars). Personal, specific, not salesy.

---

### SEQUENCE — Build outreach sequence

**Command:**
```
sequence: [prospect type] · [your offer] · [channel: email / LinkedIn / mixed] · [touches: 3 / 5 / 7]
```

**Output:** Full outreach sequence with:
- Message per touch (subject, body, CTA)
- Timing between messages
- What to do if no response at each stage
- Exit condition (when to stop)

---

## SECTION C — SALES PROCESS / PROCESSUS DE VENTE

---

### DEMO-PREP — Prepare a demo

**Command:**
```
demo-prep: [prospect company] · [their role] · [what they said they care about] · [your product] · [demo length: X min]
```

**Output:**
- Opening (2 min): their world, their problem
- Demo arc (80%): show what they said they need, not everything you have
- Close (final 5 min): next step
- Questions to ask during the demo
- Likely objections + responses

---

### PROPOSAL — Write a sales proposal

**Command:**
```
proposition: [prospect] · [their problem as you understand it] · [your solution] · [scope + pricing] · [timeline]
```

**Output:** Professional proposal with: executive summary, problem, solution, investment, ROI framing, next steps.

---

### OBJECTION — Handle an objection

**Command:**
```
objection: [exact words of the objection] · [context: deal stage, what you've already said]
```

**Output:** Response framework: acknowledge → reframe → evidence → next step. Not a script — a structure.

**Common solo founder objections:**
- "You're too small / just one person" → `objection: vous êtes trop petit`
- "We need to think about it" → `objection: on doit y réfléchir`
- "Too expensive" → `objection: c'est trop cher`
- "We already have a solution" → `objection: on a déjà quelque chose`

---

### FOLLOW-UP — Follow up after silence

**Command:**
```
follow-up: [context: what happened, when] · [how long since last contact] · [what you want as next step]
```

**Output:** Follow-up that adds value. Not "just checking in."

---

### CRM-NOTE — Log a sales interaction

**Command:**
```
crm-note: [rough notes from call or meeting] · [outcome] · [next steps agreed]
```

**Output:** Clean CRM entry with: summary, sentiment, commitments, next actions with dates.

---

### CLOSE — Draft a closing message

**Command:**
```
close: [deal context] · [where you are in the conversation] · [what needs to happen to move forward]
```

**Output:** Closing message that removes friction, makes the next step obvious, and doesn't pressure.

---

## SECTION D — PIPELINE MANAGEMENT

---

### PIPELINE — Review your pipeline

**Command:**
```
pipeline: [list your deals: name, stage, size, last contact, next step]
```

**Output:**
- Deals ranked by probability × value
- Stale deals flagged (no activity in X days)
- Missing next steps identified
- Recommended focus for the week (top 3 deals to move)

---

### FORECAST — Sales forecast

**Command:**
```
forecast-ventes: [deals in pipeline with stage and amount] · [close rate assumption] · [period: this month / Q]
```

**Output:** Forecast with: best case / expected / worst case. What needs to close to hit target.

---

## QUICK REFERENCE / RÉFÉRENCE RAPIDE

```
lead-scan           → leads by offer + sector + triggers
lead-scan-sector    → pre-built sector scan (8 sectors)
icp                 → ideal customer profile
prospect            → research a specific company
cold-email          → cold email under 100 words
linkedin            → LinkedIn outreach note
sequence            → multi-touch outreach sequence
demo-prep           → demo preparation
proposition         → sales proposal
objection           → objection handling
follow-up           → follow-up after silence
crm-note            → CRM log
close               → closing message
pipeline            → pipeline review
forecast-ventes     → sales forecast
```

---

## THE SOLO FOUNDER SALES TRUTH

You don't need a sales team. You need a system.

A system means:
- You know your ICP (you're not selling to everyone)
- You have a repeatable outreach sequence
- Every conversation goes into the CRM (even if it's just a markdown file)
- You follow up more than feels comfortable
- You close by making the next step obvious, not by pressuring

With this file, you have the system. What you need now is the reps.

---

*Enter-Game Solofounder · 02-VENTES · v1.1*
