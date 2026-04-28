# QUICKSTART.md
## From Zero to First Session in Under 1 Hour

**Enter-Game · v1.1 · April 2026**

---

> This document has one job: get you operational.
> Not inspired. Not informed. Operational.
> Follow the steps in order. Don't skip.

---

## WHAT YOU'LL HAVE AT THE END

- A GitHub memory repo that gives Claude persistent context
- A CLAUDE.md loaded automatically in every session
- Your first session running with the command protocol
- The enter-game hub on your phone for mobile capture

**Time required:** 45–60 minutes (one-time setup)

---

## PREREQUISITES

- GitHub account
- Claude account (claude.ai or API)
- A phone with Chrome (for mobile capture)
- Something you're actually building (project, company, experiment)

---

## STEP 1 — CREATE YOUR MEMORY REPO (10 min)

**1a.** Create a new **private** GitHub repo.
Name suggestion: `my-memory` or `[yourname]-memory`

**1b.** Clone the templates from Enter-Game:
```bash
# From the Enter-Game repo, copy the templates folder
cp -r enter-game/templates/* your-memory-repo/
```

Or manually create these 3 files in your new repo:
- `CONTEXT.md` (from `templates/CONTEXT.md`)
- `RECENT.md` (from `templates/RECENT.md`)
- `CLAUDE.md` (from `templates/CLAUDE.md`)

**1c.** Fill in CONTEXT.md.
Replace every `[bracket]` with real information about your project.
Target: 10–15 minutes. Be concise. This is working memory, not a business plan.

**1d.** Fill in CLAUDE.md.
5 minutes. The key fields: who you are, your project, your working style.

**1e.** Commit and push.
```bash
git add . && git commit -m "init: enter-game memory setup" && git push
```

✓ **Checkpoint:** Your memory repo exists on GitHub with 3 populated files.

---

## STEP 2 — SET UP CLAUDE (10 min)

**Option A — Claude.ai Projects (recommended)**
1. Go to claude.ai → Projects → New Project
2. Name it after your main project
3. In Project Instructions, paste the content of your CLAUDE.md
4. Upload CONTEXT.md and RECENT.md as project files
5. Claude will load them automatically every session

**Option B — Cowork / Claude Desktop**
1. Place your CLAUDE.md in your workspace folder (the folder you've selected in Cowork)
2. Claude reads it automatically on startup
3. For CONTEXT.md + RECENT.md: reference them in your CLAUDE.md or load manually

**Option C — API / Claude Code**
1. Place CLAUDE.md in your project root
2. Claude Code loads it automatically
3. CONTEXT.md and RECENT.md load via the memory protocol in CLAUDE.md

✓ **Checkpoint:** Claude knows who you are without you explaining.

---

## STEP 3 — RUN YOUR FIRST SESSION (15 min)

Open Claude. Type:

```
contexte
```

Claude should respond with a summary of your current state from CONTEXT.md + RECENT.md.
If it doesn't know anything, your files aren't loaded — go back to Step 2.

Now type:

```
interview-moi sur [la chose la plus importante sur laquelle tu travailles en ce moment]
```

Claude will ask 5–8 questions. Answer them. This is your first real session.

End with:

```
handoff
```

Claude will log the session decisions and tell you what to update in RECENT.md.
Update it manually for now (automation comes later).

✓ **Checkpoint:** You've completed a full session with context load → work → handoff.

---

## STEP 4 — INSTALL THE MOBILE HUB (10 min)

The enter-game hub lets you capture ideas from your phone with one button.

**4a.** Deploy the hub to GitHub Pages:
1. Rename `enter-game-hub-v2.html` to `index.html`
2. Push it to a new public repo named `enter-game` (or any name)
3. GitHub Settings → Pages → Source: main → Save
4. Your URL: `https://[yourusername].github.io/enter-game`

**4b.** Configure the hub:
1. Open the URL on your phone
2. Go to Config tab
3. Enter your GitHub token (needs `repo` write permission)
4. Test the connection

**4c.** Add to home screen:
- Chrome (Android): Menu → Add to Home Screen
- Safari (iOS): Share → Add to Home Screen

**4d.** Test it:
Type any idea. Select a tag. Hit Save.
Check your GitHub repo — the idea should be there as a .md file.

✓ **Checkpoint:** You can capture an idea from your phone in under 10 seconds.

---

## STEP 5 — USE THE COMMAND PROTOCOL (5 min)

Open `COMMANDS.md`. Read Tier 1 and Tier 2. That's what you need for the first week.

Your daily pattern:
```
Morning:  contexte → standup → go [top priority]
During:   idée [anything that comes up] → back to work
Evening:  handoff
```

Don't try to use all commands at once. Add one new command per week until they're automatic.

✓ **Checkpoint:** You have a daily rhythm.

---

## WHAT COMES NEXT / CE QUI VIENT ENSUITE

**Week 1:** Daily session protocol (context → work → handoff)
**Week 2:** Add mobile capture to your routine
**Week 3:** Start using Tier 3 build commands (spec, docs, revue)
**Week 4:** First MetaObserver scan — run `métaobs` and check system health

**Level 3 (coming):** Claude integrated directly in the capture loop — idea → structure → push, without manual formatting.

---

## IF SOMETHING DOESN'T WORK

**Claude doesn't know my context:**
→ CLAUDE.md isn't loaded. Check Step 2 for your setup method.

**GitHub push fails in the hub:**
→ Token permissions. Make sure the token has `repo` write scope.

**Handoff doesn't update RECENT.md automatically:**
→ Manual update for now. Copy Claude's handoff output into RECENT.md, commit, push.
→ Full automation is in the roadmap (GitHub Actions, Step 6 coming).

**I have more than 3 priorities:**
→ Drop something. If everything is priority, nothing is.

---

## THE ONE RULE / LA RÈGLE UNIQUE

> No session ends without a handoff.

If you respect only one thing from this entire protocol, make it this.
The handoff is what transforms individual sessions into a compounding system.

---

*Enter-Game · v1.1 · "You don't start a company. You enter the game."*
*github.com/[yourusername]/enter-game*
