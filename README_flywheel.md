# README_flywheel.md
## The Enter-Game Flywheel / Le Flywheel Enter-Game

**Enter-Game · v1.0 · April 2026**

---

> Publishing a repo is not distribution.
> Distribution is when every user becomes a node in your propagation network.
> This document builds that machine.
>
> *Publier un repo n'est pas de la distribution.
> La distribution, c'est quand chaque utilisateur devient un nœud dans ton réseau de propagation.
> Ce document construit cette machine.*

---

## TWO READING MODES / DEUX MODES DE LECTURE

| 🛠️ **DEV BRANCH** | 🧭 **NON-DEV BRANCH** |
|---|---|
| GitHub Actions tracking, badge system, template repo mechanics, contribution architecture | "Your success is the ad for Enter-Game" — the propagation loop explained |

---

## THE PROBLEM WITH PASSIVE DISTRIBUTION / LE PROBLÈME DE LA DISTRIBUTION PASSIVE

### [NON-DEV]

Most open-source protocols die quietly. Someone builds something useful, posts it on GitHub, and waits. A few stars. A few forks. Then silence.

Why? Because **publishing ≠ distribution**.

The standard logic: build → publish → people find it → they adopt.

The failure point: "people find it." In 2026, there are 300M+ GitHub repos. Being on GitHub doesn't mean being found. And being found doesn't mean being used. And being used once doesn't mean being adopted.

The frontier logic: build → publish → each user generates visible proof → proof attracts next user → each new user amplifies the proof → the loop accelerates.

The difference is **propagation by proof**. Your success becomes the ad. Their success becomes the next ad. No marketing budget. No SEO campaign. No influencer collab. Just visible results that make the next person say "I want that."

---

### [DEV]

**What's missing in most open-source protocol repos:**
1. No first-value moment (user can't get a result in < 24h)
2. No proof-sharing mechanism (results invisible to the network)
3. No contribution-to-improvement loop (users can improve but few do)
4. No network effects (each user's experience is isolated)

Enter-Game flywheel design addresses all four.

---

## THE FLYWHEEL MECHANISM / LE MÉCANISME DU FLYWHEEL

```
          ┌──────────────────────────────────┐
          │         NEW USER FORKS           │
          └──────────────┬───────────────────┘
                         │
                         ▼
          ┌──────────────────────────────────┐
          │    SETS UP IN < 1 HOUR           │
          │  (template does the heavy work)  │
          └──────────────┬───────────────────┘
                         │
                         ▼
          ┌──────────────────────────────────┐
          │  GETS FIRST VISIBLE RESULT       │
          │       IN < 24 HOURS              │
          └──────────────┬───────────────────┘
                         │
                         ▼
          ┌──────────────────────────────────┐
          │   SHARES RESULT (natural urge)   │
          │  GitHub · X · community · team   │
          └──────────────┬───────────────────┘
                         │
                         ▼
          ┌──────────────────────────────────┐
          │  SOMEONE SEES THE PROOF          │
          │  AND WANTS THE SAME RESULT       │
          └──────────────┬───────────────────┘
                         │
                         ▼
          ┌──────────────────────────────────┐
          │       NEW USER FORKS  ◄──────────┘
          └──────────────────────────────────┘
```

**The four accelerators that spin the flywheel faster:**
1. Shorter time-to-first-value (faster setup = more completions)
2. Better proof artifacts (clearer results = more shares)
3. Active contribution loop (users improve protocol = better results for everyone)
4. Community nodes (power users who evangelize organically)

---

## THE 4 FLYWHEEL COMPONENTS / LES 4 COMPOSANTES DU FLYWHEEL

---

### Component 1 — First Value in < 24h / Première Valeur en < 24h

**[NON-DEV]:** The single most important design constraint. If a new user can't get a meaningful result in their first day, they leave and never come back. The protocol must be set up and producing visible output in under 24 hours from the moment someone forks the repo.

**The minimum viable first result:**
```
Day 1 — You fork Enter-Game.
       You create your CONTEXT.md (template provided — 20 minutes).
       You upload it to your AI project.
       You run your first batched session.
Result: You shipped something you'd have taken 3x longer to do without the protocol.
```

That's the proof. It's specific. It's measurable. It's yours.

**[DEV] Template repo mechanics:**

The Enter-Game template provides a working CONTEXT.md, TODO.md, and the memory architecture pre-built. Fork → fill in your info → start. No setup from scratch.

```bash
# One-command setup
gh repo create your-name-memory --template yoanMaisonneuve/Enter-Game-template --private
cd your-name-memory
cp templates/CONTEXT.md .
# Edit CONTEXT.md with your info (20 min)
git add -A && git commit -m "init: personal memory setup"
git push origin main
```

**GitHub template repo configuration:**
```
Repository settings → Check "Template repository"
Add: .github/ISSUE_TEMPLATE/first-result.md
Add: templates/CONTEXT.md (pre-filled with [PLACEHOLDER] markers)
Add: setup.sh (automates directory creation and initial commit)
```

---

### Component 2 — Visible Proof Artifacts / Artefacts de Preuve Visibles

**[NON-DEV]:** Results that aren't visible don't propagate. The flywheel requires each user's results to be shareable — not just "I feel more productive" but concrete, visible proof.

**What good proof looks like:**
- "I shipped X in Y time using Enter-Game (vs my previous Z time)"
- "My agent pipeline handled [task type] autonomously — here's the output"
- "I went from idea to deployed in [timeframe] — here's what I used"

**The share trigger:** People share things that make them look competent and that they believe others will find valuable. A result that says "I did in 2 hours what would have taken my team 2 days" is shareable. A result that says "my AI is helpful" is not.

**[DEV] Case study template (case-studies/ folder):**

```markdown
# Case Study — [Your name] — [Date]

## What I built
[One-line description]

## The Enter-Game components used
- [ ] 7-agent pipeline
- [ ] Memory architecture (L1–L4)
- [ ] Voice-first protocol
- [ ] Batch execution
- [ ] Other: ___

## The result
- Time to ship: [X hours/days]
- Without Enter-Game (estimated): [Y hours/days]
- Multiplier: [Y/X]x

## What was surprising
[One thing that worked better than expected]

## One thing to improve
[Honest feedback for the protocol]

## Links (optional)
[Your repo, product, tweet, etc.]
```

**Contributing a case study = contributing to the flywheel.** Each case study makes the repo stronger evidence that the protocol works.

---

### Component 3 — The Contribution Loop / La Boucle de Contribution

**[NON-DEV]:** The protocol improves every time a user contributes. If Enter-Game is a static document, it decays — the world moves, the protocol stays still. If users contribute their improvements, the protocol evolves with the people using it.

**Types of contributions:**

| Type | What it is | Effort |
|---|---|---|
| Case study | Document your results | 30 min |
| Protocol improvement | Better way to do something specific | 1–2 hours |
| New agent variant | Specialized agent for a domain | Half day |
| Tool integration | How to connect Enter-Game to a specific tool | Half day |
| Translation | Protocol in a new language | 1 day |

**The contribution standard:** Document what you do, why it works, and what it replaced. No contribution without evidence.

**[DEV] Contribution review process:**

```
PR submitted
→ Automated check: does it follow template format?
→ Human review (maintainer): does the claim have evidence?
→ If approved: merged + contributor credited in CONTRIBUTORS.md
→ If not: feedback provided, PR stays open
```

**GitHub PR template (.github/PULL_REQUEST_TEMPLATE.md):**
```markdown
## What this PR changes
[Describe the protocol improvement or addition]

## Evidence it works
[How did you test this? What were the results?]

## What it replaces (if applicable)
[Previous approach + why this is better]

## Branch
- [ ] Dev branch (technical, with code)
- [ ] Non-dev branch (plain language)
- [ ] Both
```

---

### Component 4 — Network Nodes / Nœuds du Réseau

**[NON-DEV]:** Power users become evangelists — not because they're asked to, but because the protocol gave them results and they want others to have the same results. These are the highest-leverage distribution nodes: people who use Enter-Game and talk about it in their natural contexts (communities, newsletters, team chats, social media).

**How to identify power user nodes:** They're the ones who:
- Contributed at least one PR
- Have an active fork (not just starred)
- Showed up in a community thread with their results

**How to support them:** Feature their case studies. Acknowledge their contributions. Nothing else required — the protocol does the rest.

---

## DISTRIBUTION CHANNELS / CANAUX DE DISTRIBUTION

### Organic channels (no cost, compound over time)

| Channel | Why it works | How to activate |
|---|---|---|
| GitHub stars → forks | Discovery mechanism built into the platform | Quality repo + case studies |
| Community mentions | Builders talk to builders | Power user nodes |
| Tweets/posts with results | Social proof at scale | Case study template |
| Newsletter inclusions | High trust, targeted audience | Reach out when results are documented |
| Fork → adapt → credit | Natural propagation | Template repo + contribution norms |

### The three communities where Enter-Game propagates fastest

**Dev communities:** Hacker News, r/MachineLearning, r/LocalLLaMA, GitHub Explore
→ Lead with technical depth. Show the agent architecture, the memory implementation, the MetaObserver.

**Solo founder communities:** Indie Hackers, r/EntrepreneurRideAlong, Starter Story
→ Lead with the economic result. "$X in Y time, 1 person, agents did the rest."

**AI builder communities:** X/Twitter AI builder threads, specific Discord servers (Agent Protocol, LangChain, etc.)
→ Lead with the protocol gaps you're solving. Voice → dispatch async. MetaObserver. The frontier stuff.

---

## FLYWHEEL METRICS / MÉTRIQUES DU FLYWHEEL

### What to track / Quoi mesurer

| Metric | Target | Why |
|---|---|---|
| Time to first result (new user) | < 24 hours | Leading indicator of flywheel friction |
| Fork-to-active ratio | > 30% | Are people actually using it (not just cloning) |
| Case studies submitted | 1+/month | Proof generation rate |
| Active forks (commits in 30 days) | > 100 | Real adoption signal |
| Community mentions | Trending | Awareness |
| PR contributions | 1+/week at scale | Protocol improvement rate |

### Progression benchmarks / Jalons de progression

| Level | Signal | Flywheel state |
|---|---|---|
| Seed | 10 forks, 3 case studies | Barely spinning |
| Growing | 100 active forks, 10 case studies | Spinning — proof is visible |
| Scaling | 500 active forks, Enter-Game mentioned in 5+ communities | Self-sustaining propagation |
| N5 | Referenced in 10+ communities, contributions from strangers | Planetary distribution |

---

## THE ANTI-VIRALITY PRINCIPLE / LE PRINCIPE ANTI-VIRALITÉ

### [NON-DEV]

Enter-Game is not designed to go viral. Viral = fast and shallow. The flywheel target is something different: **sticky and deep**.

The ideal Enter-Game user is not someone who sees a tweet, gets excited, forks the repo, and forgets about it in a week. The ideal user is someone who implements the protocol, gets results, makes it their own, and still uses it 6 months later.

This requires the first-value moment to be real, not just impressive-looking. It requires the protocol to actually work in their context, not just in the context it was designed for. And it requires the contribution loop to let them adapt it until it does.

Slow is fine. What matters is that the people who use it don't leave.

---

### [DEV] Design Principles That Prevent Churn

```
1. Template > tutorial
   A template you fill in is used. A tutorial you read is forgotten.
   Enter-Game provides templates for CONTEXT.md, RECENT.md, every agent prompt.

2. First session success guarantee
   The protocol must produce a visible result in session 1.
   If it doesn't, identify the step that failed and fix the template.

3. Modularity
   Users who don't want voice-first can skip README_voicefirst.md.
   Users who don't want multi-agent can start with just the memory architecture.
   The full protocol is optional layers on top of a minimal working core.

4. Anti-lock-in
   No tool in the protocol is mandatory. Claude? Swap for GPT. GitHub? Swap for GitLab.
   The protocol is the structure, not the tools. Tools are implementation details.
```

---

## THE MISSION LINK / LE LIEN AVEC LA MISSION

**[NON-DEV]** The flywheel is not just a growth mechanism. It's the mechanism by which Enter-Game fulfills its deeper purpose.

The protocol was built because high-performance operating environments — the kind that let a single person build and ship what would take a traditional team — are not evenly distributed. They emerge from proximity to knowledge, capital, communities, and feedback loops that most people don't have access to.

Enter-Game is the attempt to distribute that access. Not to explain it — to give it. A working system that anyone can fork, implement, and use.

The flywheel is the engine of that distribution. Every active fork is one more person operating at a level they couldn't before. Every case study is one more proof that this is accessible, not just possible.

That's what the flywheel is for.

---

*Enter-Game · README_flywheel.md · v1.0 · April 2026*
