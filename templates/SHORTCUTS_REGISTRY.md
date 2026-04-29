# SHORTCUTS_REGISTRY.md
## Mon Registre de Commandes Courtes / My Shorthand Registry

> Ce fichier est lu automatiquement depuis ton CLAUDE.md.
> Ajoute, modifie, supprime des entrées librement.
> C'est ton langage personnel avec Claude.

*Dernière mise à jour : [YYYY-MM-DD]*

---

## COMMENT ÇA FONCTIONNE / HOW IT WORKS

**Syntaxe :**
- `Git/[nom]` → switch de contexte vers ce projet (charge le CLAUDE.md correspondant)
- `/[commande]` → exécute la tâche définie ci-dessous
- `/[commande]: [params]` → tâche avec paramètres additionnels

**Règle pour Claude :**
Si une commande n'est pas dans ce registre → demander :
"Je ne reconnais pas `/[commande]`. Veux-tu que je l'ajoute au registre ?"

---

## PROJECTS / PROJETS

*(Remplis avec tes projets actifs. Un projet = une entrée.)*

```
Git/Enter-Game:
  file: Enter-Game/Claude_init/CLAUDE.md
  description: Protocole IA open-source, skills library, solofounder OS

Git/Blueprint:
  file: Blueprint-memory/Claude_init/CLAUDE.md
  description: Blueprint memory system — mémoire hiérarchique scalable

Git/askio1-llm:
  file: askio1-llm/Claude_init/CLAUDE.md
  description: LLM visionnaire fine-tuné sur corpus Forsight — 3 phases (foundations → dataset → fine-tune)

Git/the-grid:
  file: the-grid/Claude_init/CLAUDE.md
  description: Réseau d'intelligence directionnelle — 14 secteurs 3D, agents, newsletter, publication d'impact

Git/chantier-3d:
  file: chantier-3d/Claude_init/CLAUDE.md
  description: Plateforme gestion chantier — photo→rapport, carte territoire, approvisionnement, soumissions

Git/[ton-projet]:
  file: [chemin/vers/CLAUDE.md]
  description: [description]
```

---

## DAILY TASKS / TÂCHES QUOTIDIENNES

*(Les tâches que tu fais souvent. Ajoute les tiennes.)*

```
/vidéo du jour:
  action: Chercher les meilleures vidéos IA publiées aujourd'hui ou hier (YouTube, X, newsletters)
  output: Liste numérotée — titre + URL + 1 ligne de contexte + pourquoi ça compte
  destination: Créer un fichier journal/daily/YYYY-MM-DD-videos.md OU afficher dans le chat si pas de dossier journal
  description: Top vidéos IA du jour

/news IA:
  action: Chercher les news IA importantes des dernières 24h
  sources: Anthropic blog, OpenAI blog, HackerNews, X/Twitter AI, TechCrunch
  output: Briefing — 5 à 10 items, format : [TITRE] · [SOURCE] · [résumé 2 lignes] · [impact pour toi]
  destination: journal/daily/YYYY-MM-DD-news.md OU chat si pas de journal
  description: Briefing IA du matin

/semaine IA:
  action: Synthèse des 5 événements IA les plus importants des 7 derniers jours
  output: Doc avec titre, ce qui s'est passé, et ce que ça change
  destination: journal/weekly/YYYY-WNN-recap.md OU chat
  description: Recap hebdomadaire IA

/standup:
  action: Générer le standup du jour depuis l'activité récente chargée en contexte
  output: Format 3 lignes — Hier · Aujourd'hui · Bloqueurs
  destination: Chat (copier-coller dans Slack/Teams)
  description: Daily standup

/handoff:
  action: Archiver la session — log des décisions, update RECENT.md, confirmer commit
  output: Résumé de session + confirmation
  destination: RECENT.md (update) + GitHub commit si demandé
  description: Fin de session, archivage mémoire
```

---

## WEEKLY TASKS / TÂCHES HEBDOMADAIRES

```
/revue semaine:
  action: Faire le bilan de la semaine depuis RECENT.md et les notes de session
  output: Wins · Misses · Décisions prises · Priorités semaine prochaine
  destination: Chat
  description: Revue hebdomadaire

/plan semaine:
  action: Planifier la semaine à venir depuis les tâches en cours et les priorités
  output: Top 3 priorités + plan par jour (lundi-vendredi)
  destination: Chat
  description: Planning hebdomadaire
```

---

## ON-DEMAND TASKS / TÂCHES À LA DEMANDE

```
/projet: [nom]:
  action: |
    1. Créer la structure de dossier locale :
       openClaude/[nom]/
       openClaude/[nom]/Claude_init/CLAUDE.md     ← mémoire opérationnelle
       openClaude/[nom]/Claude_init/claudetodo.md ← tâches en cours
       openClaude/[nom]/README.md                 ← description du projet
    2. Remplir CLAUDE.md avec le template projet :
       - Qui est Yoan / style de travail (copié depuis Enter-Game/CLAUDE.md)
       - Ce qu'est le projet (vision, mantra, public cible)
       - Structure du repo (à remplir au fur et à mesure)
       - Décisions prises (tableau vide)
       - Ce qui manque encore (à remplir)
       - Shorthand protocol (lien vers registre Enter-Game)
    3. Remplir claudetodo.md avec une entrée initiale "Setup du projet"
    4. Ajouter l'entrée Git/[nom] dans Enter-Game/templates/SHORTCUTS_REGISTRY.md
    5. Confirmer : "✓ Projet [nom] créé — structure prête, Git/[nom] actif"
  output: Dossier projet initialisé + CLAUDE.md + claudetodo.md + README.md + raccourci Git/[nom]
  destination: openClaude/[nom]/ (local)
  description: Crée un nouveau projet avec structure standard et l'enregistre dans le registre

/rapport: [sujet]:
  action: Écrire un rapport sur le sujet fourni
  output: Document structuré (intro + sections + conclusion)
  destination: journal/rapports/YYYY-MM-DD-[sujet].md
  description: Rapport structuré à la demande

/résumé: [contenu]:
  action: Résumer le contenu fourni (coller un article, des notes, un transcript)
  output: 3 lignes clés + 1 paragraphe si demandé
  destination: Chat
  description: Résumé rapide

/idée: [texte]:
  action: Structurer l'idée + push vers GitHub (repo configuré dans CLAUDE.md)
  output: Fichier .md créé dans ideas/YYYY-MM-DD-[tag].md
  destination: GitHub
  description: Capture d'idée vers GitHub

/interview: [sujet]:
  action: Poser 5-8 questions sur ce que je n'ai pas considéré
  output: Questions dans le chat, attendre mes réponses
  destination: Chat
  description: Interview pré-décision

/forsight: [texte brut]:
  action: |
    1. Déterminer le prochain numéro F — lire le dossier Forsight/ local ou le repo GitHub
       pour trouver le dernier numéro et incrémenter (F001 → F002 → F003...)
    2. Reformuler le texte brut (voice-to-text, notes, idée rapide) en post LinkedIn publiable :
       - Titre accrocheur avec numéro et thème
       - Corps 200–400 mots, ton direct, structure : problème → insight → implication
       - Dernière ligne = formule transmissible (italique)
       - Hashtags : #keepTrackFeedChangeByForsight + 3-4 hashtags pertinents
    3. Créer le fichier F[NNN]-[YYYY-MM-DD]-[description-compacte-en-kebab-case].md
       Contenu : idée brute originale (section "Idée brute") + version publiée (section "Version publiée")
    4. Sauvegarder localement dans Forsight/
    5. Push vers github.com/[ton-username]/Forsight via git ou API GitHub
    6. Logger dans Blueprint-memory (lightweight, sans charger l'arbre mémoire) :
       - Chemin cible : memory/YYYY/QN/MM-mois/WNN/YYYY-MM-DD/
         (calculé depuis la date du jour — ex: 2026-04-29 → 2026/Q2/04-avril/W18/2026-04-29/)
       - Si INDEX-jour.md existe → ajouter 1 ligne au tableau des sessions
       - Si INDEX-jour.md n'existe pas → créer le fichier minimaliste avec cette première entrée
       - Format de la ligne : | S→ | /forsight [titre court] | F[NNN] créée + push Forsight | CAPTURE |
       - Push via API GitHub (Blueprint-memory repo, même token)
       - Pas de chargement de l'arbre mémoire complet — juste lecture/écriture du fichier jour
    7. Confirmer : "✓ F[NNN] enregistrée — [titre court] · mémoire loggée"
  output: Post LinkedIn reformulé dans le chat + fichier .md créé + push Forsight + entrée mémoire
  destination: Forsight/ (local) + github.com/yoanMaisonneuve/Forsight (public) + Blueprint-memory/memory/ (privé)
  description: Capture, reformule, publie une foresight datée ET la logue dans la mémoire durable
```

---

## COMMENT AJOUTER UNE ENTRÉE / HOW TO ADD AN ENTRY

**Modèle / Template :**
```
/[ma-commande]:
  action: [ce que Claude fait — en 1–2 phrases]
  sources: [où Claude cherche l'info, si applicable]
  output: [format du résultat]
  destination: [où ça va : chat / fichier / GitHub]
  description: [1 ligne pour l'index]
```

**Exemple personnel :**
```
/clients du jour:
  action: Depuis les notes chargées en contexte, résumer les interactions clients d'aujourd'hui
  output: Liste des clients contactés + état + prochaine étape
  destination: Chat
  description: Résumé client quotidien
```

**Règle :** si tu dis une commande plus de 3 fois, crée une entrée dans ce registre.

---

## COMMANDES INTÉGRÉES (pas dans le registre)

Ces commandes fonctionnent toujours, sans être dans le registre :

```
contexte    → charge CONTEXT.md + RECENT.md, résume l'état actuel
go [tâche]  → exécute immédiatement, sans préambule
handoff     → archive la session
mémoire [X] → sauvegarder un fait en mémoire
```

---

*SHORTCUTS_REGISTRY.md — personnalise librement · v1.0 · Enter-Game*
