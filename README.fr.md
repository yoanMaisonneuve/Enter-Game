# enter-game

> **On ne crée pas une entreprise. On entre dans le jeu.**

Un protocole open-source pour les fondateurs solos qui construisent avec un agent IA comme co-fondateur.

🇬🇧 English version: [README.md](README.md)

---

## Pourquoi ce repo existe

La plupart des guides pour fondateurs sont écrits pour des équipes. Dynamique d'équipe, recrutement, management, investisseurs.

Mais une nouvelle catégorie existe maintenant : **le builder solo avec un agent IA comme co-fondateur**. Un humain. Un modèle. Un compte GitHub. Un cluster. C'est toute l'entreprise.

Ce setup n'est pas une "startup light". C'est un autre jeu — avec d'autres bottlenecks, d'autres leviers, d'autres modes d'échec.

`enter-game` documente ce jeu. Les protocoles, l'architecture, les pièges, les avantages asymétriques.

---

## La thèse centrale

> Le vrai bottleneck n'est pas le compute. C'est l'humain qui nourrit le modèle en contexte.

Les GPUs sont inactifs la majorité de la journée. Les modèles écrivent du code plus vite que n'importe quelle équipe. Ce qui est lent, c'est l'humain — décider ce qui compte, cadrer le problème, valider l'output, commiter le résultat.

Si tu optimises le handshake humain-IA, tout le reste accélère.

- RAND 2025 : **80–90% des projets agents échouent en production** — cause racine : mauvais contexte.
- Karpathy : **les tokens inactifs = tu es le bottleneck.**
- Les gagnants construisent des systèmes, pas des prompts.

---

## Les 5 principes — CAPGS

**C — Contexte d'abord, toujours.**
Aucune tâche ne démarre sans le bon contexte chargé. Un petit `CONTEXT.md` lu en début de session bat un prompt de 10 000 tokens à chaque fois.

**A — Autonomie sur les détails, validation sur l'architecture.**
Le modèle exécute le tactique. L'humain valide le gros (architecture, déploiements prod, budgets).

**P — Parallélisme par défaut.**
Batcher les tâches dans un seul message. Trois prompts séparés = trois chargements de contexte. Un prompt batché = un chargement.

**G — GitHub = source de vérité unique.**
Pas Notion. Pas Google Drive. Pas un dossier local. Tout passe par Git.

**S — Spécificité > Généralité.**
Un prompt spécifique avec un exemple concret bat un prompt générique. Toujours donner la cible *et* le contre-exemple.

---

## Le pipeline

```
GRAIN → INTERFACE → TRIAGE → MODÈLE → MÉMOIRE → CONTEXTE GLOBAL → ACTION → FEEDBACK
```

Voir [PIPELINE.md](PIPELINE.md) pour le détail stage-par-stage.

L'interface aujourd'hui = la voix (un casque audio). Voir [EXTERNAL-CONDITION-CONTEXT.md](EXTERNAL-CONDITION-CONTEXT.md) pour l'évolution prévue — et pourquoi chaque amélioration de bande passante d'interface améliore directement le throughput du système complet.

---

## Le set court de commandes

Un builder solo avec un modèle a besoin d'un vocabulaire — commandes courtes, sans ambiguïté.

| Commande | Effet |
|---|---|
| `go [tâche]` | Exécute |
| `stop` | Arrête + sauvegarde l'état |
| `status` | État actuel + coût |
| `commit [msg]` | Push vers le repo mémoire |
| `rapport` | Résumé session + maj TODO + commit |
| `[A] + [B] + [C]` | Batche 3 tâches en un context window |
| `interview-moi sur [X]` | Pose-moi 5–8 questions avant d'agir |
| `contexte ?` | Recharge la mémoire, résume l'état |
| `deploy [app] prod` | Demande confirmation, puis déploie |

---

## L'architecture mémoire

```
your-memory-repo/  (privé)
├── CONTEXT.md          # < 60 lignes — chargé chaque session
├── TODO.md             # liste vivante
├── DECISIONS.md        # log daté des décisions verrouillées
├── SESSION_LOG.md      # résumés auto des sessions
├── projects/           # un fichier par projet actif
├── config/             # configs infra
└── workflow/           # docs du protocole de collaboration
```

Trois couches :
- **L1** : le context file. Petit. Chargé automatiquement.
- **L2** : fichiers projet et infra. Chargés à la demande.
- **L3** : les logs — TODO, DECISIONS, SESSION, ERROR. Le journal vivant.

---

## Les garde-fous

Non négociables. Ils existent parce que le modèle **va** accepter une instruction dangereuse si tu la formules bien. Les garde-fous, c'est l'adulte dans la pièce.

| Règle | Seuil |
|---|---|
| Budget max par session de training | Hard cap (le modèle s'arrête tout seul) |
| Déploiements prod | Confirmation humaine explicite obligatoire |
| Dépense imprévue > 5$ | Signaler avant d'engager |
| Datasets | Jamais transmis hors du cluster choisi |
| Actions financières (trades, transferts) | Jamais autonome — toujours l'humain |
| `.env` / secrets | Jamais commités |

---

## Entrer dans le jeu · 5 niveaux

Le protocole livre une progression — chaque niveau retire une couche de friction entre l'idée et le commit. Voir [LEVELS.md](LEVELS.md) pour le détail.

1. **N1** · Téléphone + Claude (copier-coller manuel)
2. **N2** · GitHub Codespaces (IDE dans le browser)
3. **N2.5** · **Enter the Game Hub** — le fichier [`index.html`](index.html) de ce repo. Publié sur `yoanmaisonneuve.github.io/enter-game`. Épinglé sur l'écran d'accueil du téléphone. Capture une idée, push vers n'importe lequel de tes repos, zéro terminal.
4. **N3** · Claude Dispatch (Computer Use, mains libres voix → desktop)
5. **N4** · VPS / cluster OVH (Claude sur infra always-on)
6. **N5** · Agents autonomes (mandat + budget plafonné)

Le jeu se joue à l'intersection de deux courbes — la machine qui monte en niveau, et l'humain qui apprend à déléguer. Voir la note *Human Adoption Bottleneck* dans LEVELS.md.

---

## Ce que contient ce repo

- [`README.md`](README.md) — version anglaise
- [`README.fr.md`](README.fr.md) — ce fichier
- [`LEVELS.md`](LEVELS.md) — la progression N1 → N5
- [`index.html`](index.html) — le **Enter the Game Hub**, app de capture N2.5 (tourne sur GitHub Pages)
- [`PIPELINE.md`](PIPELINE.md) — l'architecture complète Grain → Action
- [`EXTERNAL-CONDITION-CONTEXT.md`](EXTERNAL-CONDITION-CONTEXT.md) — la couche interface (aujourd'hui : casque ; demain : BCI)
- [`LICENSE`](LICENSE) — MIT
- `ideas/` — captures append-only de sessions voice
- `.github/workflows/pages.yml` — déploiement GitHub Pages

---

## Pour qui ?

- Fondateurs solos qui shippent des vrais produits avec une IA comme co-fondateur
- Indie hackers qui passent de "l'IA comme moteur de recherche" à "l'IA comme couche d'exécution"
- Builders qui veulent un protocole à voler, forker, et adapter

Pas pour : product owners corporate qui cherchent un framework. Ici c'est ground-floor, voice-first, GitHub-first. Adapte librement.

---

## Comment l'utiliser

1. **Fork** ce repo
2. **Crée un repo mémoire privé** (appelle-le comme tu veux — `memory`, `brain`, `<ton-nom>-memory`)
3. **Copie** la structure de la section architecture mémoire
4. **Remplis ton CONTEXT.md** — qui tu es, ce que tu construis, ce qui est verrouillé
5. **Charge-le** dans ton outil IA au début de chaque session
6. **Itère** — chaque point de friction est un candidat pour une nouvelle entrée de protocole

Le protocole n'est pas le but. La pratique l'est.

---

## Licence

MIT — voir [LICENSE](LICENSE).

Forke, adapte, transforme. Un crédit est apprécié. Une obligation, non.

---

## Publier le Hub sur GitHub Pages

Le fichier `index.html` est une app web autonome. Pour en faire ta surface de capture permanente :

1. **Settings → Pages** sur ton fork
2. Sous *Build and deployment*, choisis **GitHub Actions** (le workflow `.github/workflows/pages.yml` fait le reste)
3. Attends le premier run vert
4. Ouvre `https://<ton-nom>.github.io/enter-game/`
5. Onglet **Config** → colle ton username GitHub, un PAT fine-grained avec scope `Contents: write`, la liste de tes repos, ton nom et ton email d'auteur
6. Sur Android : Chrome → ⋮ → *Ajouter à l'écran d'accueil*. Sur iOS : Safari → Partager → *Sur l'écran d'accueil*. Tu as maintenant une app hub.

**Note sécurité.** Le code source du hub est public. Le token est stocké uniquement dans le `localStorage` de ton navigateur — jamais envoyé à un serveur tiers. Traite-le comme une clé imprimée sur papier : ne partage pas ton écran sur l'onglet Config, et révoque/tourne le PAT à volonté depuis `github.com/settings/tokens`.

---

## Statut

- **v1 · avril 2026** — structure en place, docs publiés, premier cas d'usage réel (EasyRead + aski01 + infra privée)
- **v1.1 · avril 2026** — app HTML Hub + doc LEVELS + déploiement Pages
- Suite : traduction bilingue complète des docs foundational · repo de templates · études de cas publiques · mode optionnel N3 Claude-in-the-loop pour le Hub

Maintainer : [Yoan Maisonneuve](https://github.com/yoanMaisonneuve).

---

*"On ne crée pas une entreprise. On entre dans le jeu."*
