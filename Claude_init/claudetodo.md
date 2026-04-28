# CLAUDETODO.md — Mes tâches en cours et à venir

*Ma liste de tâches pour le projet Enter-Game*
*Mise à jour : 2026-04-28*

---

## 🔴 CRITIQUE — À faire dès prochaine session

- [ ] **README.md racine** — La face GitHub du repo. Ce que voit le premier visiteur. Doit pointer vers QUICKSTART, skills/, solofounder/, et l'UX web. Sans ça, le flywheel ne peut pas démarrer.

- [ ] **Jouer-v2.html** — UX web navigable pour tout le contenu sans GitHub. Les gens ne naviguent pas dans GitHub. Il faut une page web qui expose : skills/, solofounder/, COMMANDS.md, QUICKSTART. Navigation simple, mobile-first, design dark Enter-Game.

---

## 🟡 IMPORTANT — Prochaines sessions

- [ ] **Migrer hub app** — `artefact/enter-game-hub-v2.html` → `Enter-Game/` ou sous-dossier `web/`. L'app de capture doit être dans le repo, pas dans artefact.

- [ ] **Level 3 : Claude dans la boucle** — Quand l'utilisateur capture une idée, Claude la structure (titre / contexte / actions) avant le push GitHub. Nécessite un backend léger (Supabase Edge Function) pour ne pas exposer la clé API dans le HTML. Décrit comme "Niveau 3" dans workflow-2.5.md mais pas construit.

- [ ] **GitHub Actions pour handoff** — Automatiser la commande `handoff` : déclencheur → update RECENT.md → commit → push. Script bash ou workflow YAML. Documenter dans README_workflow.md section [DEV].

- [ ] **Proof artifacts** — Le flywheel a besoin de preuves. Créer un dossier `examples/` avec 2–3 exemples concrets : "voici ce qu'Enter-Game a produit en 1 session". Screenshots, outputs, résultats mesurés.

---

## 🟢 BIENTÔT — Quand le reste est stable

- [ ] **GLOBAL-PLAN.md template** — Référencé dans README_workflow.md mais pas fourni. Template pour la direction long-terme (1–5 ans).

- [ ] **SESSION_LOG.md template** — Pour les utilisateurs (différent de mon log_session.md à moi). Template que chaque user peut copier dans son repo mémoire.

- [ ] **Distribution channels** — Liste concrète : quels subreddits, Slack communities, newsletters pour publier le repo. HackerNews strategy. LinkedIn angle.

- [ ] **CONTRIBUTING.md** — Pour que le flywheel puisse s'alimenter de contributions externes. Comment ajouter un skill, comment proposer un solofounder dept, comment corriger.

- [ ] **Bilingual pass** — skills/ et solofounder/ sont EN/FR mélangés. Décider d'une stratégie cohérente (bilingue comme POWERUSER.md, ou une langue par fichier).

---

## 💭 À VALIDER AVEC YOAN

- [ ] **Langue** — skills/ et solofounder/ sont EN/FR mélangé. Stratégie : tout bilingue comme POWERUSER.md ? Ou FR pour solofounder/, EN pour skills/ (enterprise) ?

- [ ] **Hub app location** — Déplacer `enter-game-hub-v2.html` de artefact/ vers Enter-Game/ ? Ou garder séparé ?

- [ ] **UX web** — Jouer-v2.html : refonte complète ou mise à jour de Jouer.html existant ? (Jouer.html = 42kb, a du contenu mais n'inclut pas skills/ et solofounder/)

- [ ] **Commentaires auto** — Feature demandée : auto-suggest commentaires en naviguant sur une section commentaires. Chrome MCP. À construire séparément ou intégré dans le hub ?

- [ ] **GitHub Pages** — Le repo est-il déployé sur GitHub Pages ? Si oui, quelle URL ?

---

## ✅ COMPLÉTÉ CETTE SESSION (2026-04-28)

- [x] Gap analysis du repo existant
- [x] COMMANDS.md — couche agentic 7 tiers
- [x] skills/08-SHORTCUTS.md — protocole shorthand complet
- [x] templates/SHORTCUTS_REGISTRY.md — registre installable
- [x] QUICKSTART.md — setup en < 1h
- [x] templates/ — CLAUDE.md + CONTEXT.md + RECENT.md
- [x] skills/ — 7 domaines enterprise, ~77 commandes
- [x] solofounder/ — 9 départements, ~70 commandes
- [x] Claude_init/ — CLAUDE.md + index.md + log_session.md + ce fichier

---

*Format des entrées : [ ] = à faire · [x] = complété · date si important*
