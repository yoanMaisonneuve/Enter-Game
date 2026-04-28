# 08 — SHORTHAND PROTOCOL
## Context Switching · Task Dispatch · Zero-Friction Commands

**Enter-Game Skills · v1.0 · April 2026**

---

> You shouldn't have to explain where you are every session.
> You shouldn't have to describe a task you run every day.
> This protocol eliminates both problems in one file.
>
> *Tu ne devrais pas avoir à expliquer où tu es à chaque session.
> Tu ne devrais pas avoir à décrire une tâche que tu fais chaque jour.
> Ce protocole élimine les deux problèmes en un seul fichier.*

---

## WHAT THIS IS / CE QUE C'EST

A **shorthand registry** — a file you install once that teaches Claude your personal command language.

After installation:
- `Git/Enter-Game` → Claude knows exactly which project, loads the right context, ready to work
- `/vidéo du jour` → Claude scans today's AI videos, produces a digest, saves it where you want
- `/news IA` → morning briefing on AI news, delivered in your format
- `/standup` → daily update generated from recent activity
- No explanation needed. No preamble. Say the word, get the output.

---

## THE SYNTAX / LA SYNTAXE

Three patterns. That's it.

```
Git/[nom]              → switch de contexte vers un projet
/[commande]            → exécuter une tâche enregistrée
/[commande]: [params]  → tâche avec paramètres
```

**Examples:**
```
Git/Enter-Game                    → switch to Enter-Game project
Git/Blueprint                     → switch to Blueprint project
/vidéo du jour                    → scan AI videos + produce digest
/news IA                          → morning AI news briefing
/standup                          → daily standup from recent activity
/handoff                          → archive session + push memory
/idée: j'ai pensé à quelque chose → capture idea to GitHub
/rapport: Q2 ventes               → generate Q2 sales report
```

---

## HOW IT WORKS / COMMENT ÇA MARCHE

The registry file (`SHORTCUTS_REGISTRY.md`) defines three things per command:
1. **What Claude does** — the action
2. **What you get** — the output format
3. **Where it goes** — the destination (file, GitHub, message, etc.)

When you type `Git/Enter-Game`, Claude:
1. Recognizes the `Git/` prefix → this is a context switch
2. Looks up `Enter-Game` in the registry → finds the CLAUDE.md to load
3. Loads that context silently
4. Confirms in one line: `✓ Enter-Game loaded — [current state summary]`

When you type `/vidéo du jour`, Claude:
1. Recognizes the `/` prefix → this is a dispatch command
2. Looks up `vidéo du jour` in the registry → finds the action spec
3. Executes: searches sources defined in the registry
4. Produces output in the defined format
5. Saves to the defined destination
6. Confirms: `✓ 7 vidéos trouvées — journal/2026-04-28-videos.md`

---

## INSTALLATION / INSTALLATION

**3 steps, 5 minutes, one-time.**

### Step 1 — Copy the registry file
Copy `templates/SHORTCUTS_REGISTRY.md` into your memory repo or project folder.

```
your-memory-repo/
├── CONTEXT.md
├── RECENT.md
├── CLAUDE.md          ← your main context file
└── SHORTCUTS_REGISTRY.md  ← add this file
```

### Step 2 — Add one line to your CLAUDE.md
In your `CLAUDE.md`, add this section:

```markdown
## SHORTHAND PROTOCOL

Shorthand registry loaded from: `SHORTCUTS_REGISTRY.md`

Rules:
- `Git/[name]` → context switch. Load the CLAUDE.md for that project silently. Confirm in one line.
- `/[command]` → dispatch. Execute the action defined in the registry. No preamble.
- If a command is not in the registry, ask: "Je ne reconnais pas `/[command]`. Veux-tu que je l'ajoute au registre?"
```

### Step 3 — Customize the registry
Open `SHORTCUTS_REGISTRY.md`. Fill in your projects under `## PROJECTS`. Add your daily tasks under `## TASKS`. The file is yours — add, remove, modify at will.

**That's it.** The protocol is live.

---

## TEACHING IT TO SOMEONE ELSE / ENSEIGNER LE PROTOCOLE

1. Send them this file + `templates/SHORTCUTS_REGISTRY.md`
2. Walk through INSTALLATION (3 steps above)
3. Show one `Git/` switch and one `/task` dispatch live
4. Let them customize the registry for their own projects and tasks

**Time to operational:** 15 minutes.
**Time to fluent:** 1 week of daily use.

---

## REGISTRY DESIGN GUIDE / GUIDE DE CONCEPTION DU REGISTRE

### When to create a Git/ entry
Every project you work on regularly. Anything you'd need to "re-explain" to Claude at the start of a session.

```
Git/[name]:
  file: path/to/CLAUDE.md    ← what to load
  description: [one line]
```

### When to create a /task entry
Any task you do more than once a week. Any task that requires more than 2 words to describe. Any task with a predictable output format.

```
/[command]:
  action: [what Claude does]
  sources: [where Claude looks — web, files, GitHub]
  output: [format: doc / list / digest / table / message]
  destination: [where to save: file path or "message"]
  description: [one line]
```

### Naming rules
- `Git/` entries: use exact project name, case-sensitive
- `/task` entries: use the phrase you'd actually say out loud
- Keep names short (2–4 words max)
- French or English — match your working language

---

## BUILT-IN TASKS / TÂCHES INTÉGRÉES

These work without the registry (built into the Enter-Game protocol):

```
/handoff       → archive session: log decisions, update RECENT.md, GitHub push
/contexte      → load current state from CONTEXT.md + RECENT.md
/standup       → daily standup from recent activity
/idée: [text]  → capture idea to GitHub
```

---

## EXAMPLE REGISTRY ENTRIES / EXEMPLES D'ENTRÉES

```markdown
## PROJECTS / PROJETS

Git/Enter-Game:
  file: Enter-Game/Claude_init/CLAUDE.md
  description: Protocole IA et skills library

Git/Blueprint:
  file: Blueprint-memory/CONTEXT.md
  description: Projet principal Blueprint

Git/askio1:
  file: openClaude/askio1_v2/CLAUDE.md
  description: Robot tripode Askio1 v2

## TASKS / TÂCHES

/vidéo du jour:
  action: Chercher les meilleures vidéos IA publiées aujourd'hui ou hier
  sources: YouTube, Twitter/X AI accounts, newsletter IA, Anthropic/OpenAI blogs
  output: Liste avec titre + URL + 1 ligne de description par vidéo
  destination: journal/daily/YYYY-MM-DD-videos.md
  description: Digest vidéos IA du jour

/news IA:
  action: Chercher les news IA importantes des dernières 24h
  sources: Anthropic blog, OpenAI blog, HackerNews, Twitter/X, TechCrunch AI
  output: Briefing structuré (5-10 items, titre + résumé + impact)
  destination: journal/daily/YYYY-MM-DD-news.md
  description: Briefing IA du matin

/semaine IA:
  action: Synthèse des 5 événements IA les plus importants de la semaine
  sources: Web search derniers 7 jours
  output: Doc hebdomadaire avec contexte et implications
  destination: journal/weekly/YYYY-WNN-ia-recap.md
  description: Recap IA hebdomadaire

/rapport: [sujet]:
  action: Générer un rapport sur le sujet donné
  output: Document structuré (intro, sections, conclusion)
  destination: journal/rapports/YYYY-MM-DD-[sujet].md
  description: Rapport à la demande
```

---

## ADVANCED: CHAINING / AVANCÉ : CHAÎNER LES COMMANDES

You can chain commands in one message:

```
Git/Enter-Game + /news IA + /standup
```

Claude will:
1. Load Enter-Game context
2. Run the AI news scan
3. Generate today's standup
4. Deliver all three outputs in sequence

---

## QUICK REFERENCE / RÉFÉRENCE RAPIDE

```
Git/[name]            → context switch to project
/[command]            → dispatch registered task
/[command]: [params]  → dispatch with parameters

Install:
1. Copy templates/SHORTCUTS_REGISTRY.md to your repo
2. Add shorthand rules to your CLAUDE.md
3. Customize the registry for your projects + daily tasks
```

---

*Enter-Game Skills · 08-SHORTCUTS · v1.0 · April 2026*
*"Say it once. Run it forever."*
