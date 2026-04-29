# CLAUDE.md — Enter-Game Working Context

> Ce fichier est ma mémoire opérationnelle pour le projet Enter-Game.
> Je le lis en début de session pour me situer sans qu'on m'explique tout.

---

## QUI EST YOAN / WHO IS YOAN

Yoan Maisonneuve · Solo founder · Montréal / Lorraine QC
Email: ymaisonneuve@hotmail.com

**Style de travail :**
- Voice-first (souvent en déplacement, écouteurs)
- Commandes courtes, réponses actionnables, pas de remplissage
- Autonomie totale déléguée à Claude sur les détails — validation sur les décisions majeures
- Délègue franchement : "go / soit autonome / je te délègue"
- Orientation altruiste : veut que ça serve à d'autres, pas juste à lui

---

## CE QU'EST ENTER-GAME / WHAT ENTER-GAME IS

**Vision :** Rendre accessibles les pratiques des 5% meilleurs utilisateurs IA au reste du monde — entreprises, solo founders, knowledge workers.

**Mantra :** "You don't start a company. You enter the game."

**Ce que c'est :**
- Un protocole open-source pour opérer avec l'IA comme co-fondateur permanent
- Une librairie de skills pour les fonctions d'entreprise (communication, planning, code, etc.)
- Un OS pour solo founders (9 départements d'une entreprise, seul)
- Pas juste de la documentation — du contenu immédiatement actionnable

**Public cible :**
1. Solo founders (primaire) — veulent un OS complet pour leur entreprise
2. Employés en entreprise (secondaire) — veulent des skills qui font gagner 1–2h/jour
3. Managers et équipes — veulent déployer l'IA à l'échelle sans programme de formation

**Philosophie d'adoption :**
- Zero-friction onboarding : une commande = un output
- Universal value : ça marche sans être power user
- Propagation par preuve : les résultats visibles attirent les prochains utilisateurs

---

## STRUCTURE DU REPO / REPO STRUCTURE

```
Enter-Game/
├── Claude_init/          ← MA MÉMOIRE (ce dossier)
│   ├── CLAUDE.md         ← ce fichier
│   ├── index.md          ← index de tout le repo
│   ├── log_session.md    ← log des sessions de travail
│   └── claudetodo.md     ← ma liste de tâches en cours
│
├── COMMANDS.md           ← couche agentic : les commandes par tiers
├── QUICKSTART.md         ← setup en < 1h pour nouveaux utilisateurs
├── POWERUSER.md          ← les 8 pratiques des 5% meilleurs
├── Jouer.html            ← UX web (à rafraîchir avec nouveau contenu)
│
├── README_*.md (5)       ← docs fondamentaux du protocole
│   ├── README_agents.md
│   ├── README_flywheel.md
│   ├── README_memory.md
│   ├── README_voicefirst.md
│   └── README_workflow.md
│
├── skills/               ← librairie enterprise (7 domaines)
│   ├── README.md
│   ├── 01-COMMUNICATION.md
│   ├── 02-PLANNING.md
│   ├── 03-KNOWLEDGE.md
│   ├── 04-CODE.md
│   ├── 05-PEOPLE.md
│   ├── 06-CUSTOMER.md
│   └── 07-FINANCE-OPS.md
│
├── solofounder/          ← OS solo founder (9 départements)
│   ├── README.md
│   ├── 01-CEO.md
│   ├── 02-VENTES.md
│   ├── 03-MARKETING.md
│   ├── 04-PRODUIT.md
│   ├── 05-TECH.md
│   ├── 06-OPERATIONS.md
│   ├── 07-FINANCE.md
│   ├── 08-DISTRIBUTION.md
│   └── 09-SUPPORT.md
│
└── templates/            ← starters pour nouveaux utilisateurs
    ├── CLAUDE.md
    ├── CONTEXT.md
    └── RECENT.md
```

---

## DÉCISIONS PRISES / DECISIONS MADE

| Date | Décision | Pourquoi |
|------|----------|----------|
| 2026-04-13 | Enter-Game créé comme repo protocole | Hub pour les pratiques IA solo founder |
| 2026-04-16 | Jouer.html créé (42kb, interactive) | UX pour non-GitHub users |
| 2026-04-28 | skills/ créé (7 domaines enterprise) | Adoption massive en entreprise, alignement altruiste |
| 2026-04-28 | solofounder/ créé (9 départements) | OS complet pour solo founder |
| 2026-04-28 | templates/ créé | Gap critique : aucun starter existait |
| 2026-04-28 | COMMANDS.md créé | Gap critique : zéro couche agentic |
| 2026-04-28 | QUICKSTART.md créé | Gap critique : flywheel cassé sans onboarding |

---

## CE QUI MANQUE ENCORE / WHAT'S STILL MISSING

**Priorité haute :**
- [ ] README.md racine du repo (la face GitHub — ce qu'on voit en premier)
- [ ] UX web v2 (Jouer-v2.html) — navigation sans GitHub, tout le contenu accessible
- [ ] Hub app (enter-game-hub-v2.html) dans le repo (est dans artefact/ pour l'instant)

**Priorité moyenne :**
- [ ] Level 3 : Claude dans la boucle de capture (structurer l'idée avant push)
- [ ] GitHub Actions pour handoff automatique
- [ ] Proof artifacts / démo vidéo pour le flywheel

**Priorité basse :**
- [ ] GLOBAL-PLAN.md template
- [ ] SESSION_LOG.md template
- [ ] Distribution channels spécifiques

---

## SHORTHAND PROTOCOL / PROTOCOLE DE COMMANDES COURTES

Registre chargé depuis : `../templates/SHORTCUTS_REGISTRY.md`

**Règles actives :**
- `Git/[nom]` → switch de contexte silencieux vers ce projet. Charger le CLAUDE.md correspondant. Confirmer en 1 ligne : `✓ [nom] chargé — [état en 5 mots]`
- `/[commande]` → exécuter la tâche définie dans le registre. Zéro préambule.
- `/[commande]: [params]` → idem avec paramètres
- Commande inconnue → `"Je ne reconnais pas /[commande]. L'ajouter au registre ?"`
- Commandes toujours actives sans registre : `contexte`, `go`, `handoff`, `idée`, `mémoire`

**Raccourcis projets Yoan :**
```
Git/Enter-Game  → ce repo (Claude_init/CLAUDE.md)
Git/Blueprint   → Blueprint-memory (projet principal)
Git/askio1      → robot tripode askio1_v2
```

**Raccourcis tâches actifs :**
```
/vidéo du jour     → top vidéos IA du jour → journal/daily/
/news IA           → briefing IA 24h → journal/daily/
/semaine IA        → recap 7 jours → journal/weekly/
/standup           → standup quotidien → chat
/projet: [nom]     → crée dossier + CLAUDE.md + claudetodo.md + README + enregistre Git/[nom]
/rapport: [X]      → rapport structuré → journal/rapports/
/forsight: [texte] → reformule + numérote F[NNN] + push Forsight + log mémoire Blueprint
```

**Convention Forsight :**
- Repo GitHub : github.com/yoanMaisonneuve/Forsight (public)
- Dossier local : openClaude/Forsight/
- Naming : `F[NNN]-[YYYY-MM-DD]-[description-kebab-case].md`
- Dernier numéro utilisé : F002 (2026-04-30)
- Contenu fichier : idée brute originale + version publiée
- Logging mémoire : chaque /forsight ajoute 1 ligne dans Blueprint-memory/memory/[chemin-jour]/INDEX-jour.md
  - Chemin calculé depuis date du jour, sans charger l'arbre complet
  - Type CAPTURE dans le tableau compact
  - Push via GitHub API (même token)

---

## MON PROTOCOLE DE SESSION / MY SESSION PROTOCOL

**Au démarrage :**
1. Lire ce fichier (CLAUDE.md)
2. Lire claudetodo.md pour les tâches en cours
3. Confirmer l'état avec Yoan si nécessaire

**Pendant la session :**
- Agir avec autonomie sur les détails
- Confirmer sur les décisions d'architecture ou de direction
- Logger les décisions importantes dans log_session.md

**À la fin :**
- Mettre à jour claudetodo.md
- Ajouter une entrée dans log_session.md
- Committer si demandé

---

## STYLE D'ORIENTATION / ORIENTATION STYLE

Enter-Game n'est pas un outil de productivité ordinaire.
C'est une démonstration que l'IA-comme-OS est accessible à tous — pas juste aux ingénieurs ou aux early adopters.

Quand je travaille sur ce repo, je maintiens trois tensions :
1. **Profondeur vs accessibilité** — le contenu doit être riche ET utilisable par quelqu'un qui découvre l'IA
2. **Solo vs enterprise** — deux publics très différents qui partagent les mêmes outils
3. **Protocole vs outil** — c'est un protocole (des pratiques), pas un logiciel

L'angle altruiste est central : si ce repo aide 1000 personnes à être meilleures dans leur travail,
c'est plus précieux qu'un outil payant qui aide 10 power users.

---

*Créé le 2026-04-28 · Mis à jour à chaque session*
