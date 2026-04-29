# CLAUDETODO.md — Mes tâches en cours et à venir

*Ma liste de tâches pour le projet Enter-Game*
*Mise à jour : 2026-04-29*

---

## 🔴 CRITIQUE — À faire dès prochaine session

- [ ] **Jouer-v2.html "wow"** — Design ISL appliqué (Inter, marine/vivid, cartes blanches). Yoan veut quelque chose de plus dynamique, plus percutant. Direction à valider : animations au scroll ? transitions entre tabs ? structure landing page ? À discuter au démarrage de la prochaine session.

---

## 🟡 IMPORTANT — Prochaines sessions

- [ ] **Migrer hub app** — `artefact/enter-game-hub-v2.html` → `Enter-Game/web/`. L'app de capture doit être dans le repo, pas dans artefact.

- [ ] **Proof artifacts** — Le flywheel a besoin de preuves. Créer un dossier `examples/` avec 2–3 exemples concrets : "voici ce qu'Enter-Game a produit en 1 session". Screenshots, outputs, résultats mesurés.

- [ ] **GitHub Actions pour handoff** — Automatiser la commande `handoff` : déclencheur → update RECENT.md → commit → push. Script bash ou workflow YAML.

- [ ] **Level 3 : Claude dans la boucle** — Quand l'utilisateur capture une idée, Claude la structure (titre / contexte / actions) avant le push GitHub. Nécessite un backend léger (Supabase Edge Function). Décrit dans workflow-2.5.md mais pas construit.

---

## 🟢 BIENTÔT — Quand le reste est stable

- [ ] **GLOBAL-PLAN.md template** — Référencé dans README_workflow.md mais pas fourni. Template direction long-terme (1–5 ans).

- [ ] **SESSION_LOG.md template** — Pour les utilisateurs (différent de log_session.md). Template copiable dans le repo mémoire.

- [ ] **Distribution channels** — Liste concrète : subreddits, Slack communities, newsletters. HackerNews strategy. LinkedIn angle.

- [ ] **CONTRIBUTING.md** — Comment ajouter un skill, proposer un solofounder dept, corriger.

- [ ] **Bilingual pass** — skills/ et solofounder/ sont EN/FR mélangés. Décider stratégie cohérente.

---

## 💭 À VALIDER AVEC YOAN

- [ ] **Jouer-v2 direction "wow"** — Animations ? Transitions ? Structure landing page ? (voir item critique)

- [ ] **Langue** — FR pour solofounder/, EN pour skills/ (enterprise) ? Ou tout bilingue comme POWERUSER.md ?

- [ ] **GitHub Pages home** — Remplacer index.html par Jouer-v2.html comme page d'accueil ?

- [ ] **Commentaires auto** — Feature Chrome MCP. À construire séparément ou intégré dans le hub ?

---

## ✅ COMPLÉTÉ SESSION 2026-04-28

- [x] Gap analysis du repo existant
- [x] COMMANDS.md — couche agentic 7 tiers
- [x] skills/08-SHORTCUTS.md — protocole shorthand complet
- [x] templates/SHORTCUTS_REGISTRY.md — registre installable
- [x] QUICKSTART.md — setup en < 1h
- [x] templates/ — CLAUDE.md + CONTEXT.md + RECENT.md
- [x] skills/ — 7 domaines enterprise, ~77 commandes
- [x] solofounder/ — 9 départements, ~70 commandes
- [x] Claude_init/ — CLAUDE.md + index.md + log_session.md + ce fichier

## ✅ COMPLÉTÉ SESSION 2026-04-29

- [x] Push GitHub — 29 fichiers, 4222 lignes (skills/, solofounder/, templates/, COMMANDS, QUICKSTART, Claude_init/)
- [x] README.md v1.3 — face GitHub mise à jour avec skills, solofounder, shorthand protocol, nav "Start here"
- [x] Jouer-v2.html v1 — app web navigable, 5 tabs, 150+ commandes, search, copy-to-clipboard
- [x] Jouer-v2.html v2 — redesign style ISL (Inter, marine/vivid, cartes blanches, animations fade-in)
- [x] Réconciliation local ↔ GitHub — repo cohérent, tous les fichiers GitHub existants préservés

---

*Format des entrées : [ ] = à faire · [x] = complété · date si important*
