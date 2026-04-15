# Enter the Game · The 5 Levels

> **You don't start a company. You enter the game.**

Each level removes a layer of friction between the idea in your head and its persistence on GitHub. Leveling up is not automatic — it's a deliberate upgrade that trades setup cost for compounding speed.

---

## Level 1 · Phone + Claude (manual)

**Setup** — zero. A browser, a Claude.ai tab.

**Workflow** — you dictate to Claude in chat. Claude drafts. You copy-paste into GitHub web UI, or you ask Claude to produce a shell script you run later on desktop.

**Unlocks** — nothing is ever lost inside Claude's chat. Everything lives inside a conversation.

**Friction** — every push needs a desktop visit. Ideas captured on-the-go pile up in drafts. Claude has no memory across sessions.

---

## Level 2 · GitHub Codespaces

**Setup** — enable Codespaces on your repos (free tier: 60h/month).

**Workflow** — open your repo in a browser, tap `.` (or use the "Code → Codespaces" button), edit/commit directly in the web IDE, push from the same tab.

**Unlocks** — no local git needed. Works from any device with a browser.

**Friction** — still manual file creation. No idea-capture loop. Codespaces cold-starts (10–20s). Still no cross-session memory.

---

## Level 2.5 · Enter the Game Hub 🎯 *you are here*

**Setup** — `yoanmaisonneuve.github.io/enter-game` pinned to your phone home screen. A GitHub PAT with `repo` scope pasted once in Config.

**Workflow** — open the app → type or dictate an idea → pick the target repo → one tap → the idea is a markdown file on `main`. No terminal. No IDE. No chat required.

**Unlocks** — capture latency drops from "minutes" to "seconds". You can push from a bus, from a walk, from your earbuds.

**Friction** — there is no AI in the loop yet. The hub is a thin client on top of the GitHub REST API. Claude still lives in a separate tab.

**Security model** — the PAT is stored in `localStorage` of your browser only. It is never transmitted to any server except `api.github.com`. The app's source code is public on this repo — audit it.

---

## Level 3 · Claude Dispatch (Computer Use)

**Setup** — Claude Pro subscription, Dispatch enabled (launched 2026-03-23), phone paired to desktop.

**Workflow** — from your phone, you send a voice command to Claude. Claude drives your desktop: opens VS Code, writes the file, runs the commit, pushes. You review from the bus.

**Unlocks** — "hands-free" is now real. The bottleneck shifts from typing to thinking.

**Friction** — desktop must be on. You are still the orchestrator. Claude has no persistent state outside the conversation unless you've wired `blueprint-memory` as its context file.

---

## Level 4 · Dedicated VPS / OVH cluster

**Setup** — OVH Beauharnois (`ca-east-bhs`) managed K8s cluster with a GPU node, cost-monitor hard-stop at 20 CAD, Claude running as a service with API key on the VPS.

**Workflow** — Claude lives on a machine that is always on. You send it commands via a thin chat (Telegram bot, Slack, SMS gateway). Claude runs training jobs, drafts code, pushes commits, and pings you with results.

**Unlocks** — work happens while you sleep. Your desktop state is no longer the constraint.

**Friction** — infra to maintain. A bad prompt can burn budget. Requires the 20 CAD hard-stop contract to be enforced in code, not in good intentions.

---

## Level 5 · Autonomous agents

**Setup** — a multi-step orchestrator (Claude Code + scheduled tasks + event-driven triggers) that reads your calendar, watches your repos, and takes initiative within a budget and a permission scope.

**Workflow** — you set an objective ("ship EasyRead v1.1 this week") and a budget ("200 CAD, 20h compute"). The agent plans, executes, reports, and escalates only on decisions that exceed its mandate.

**Unlocks** — the system works for you, not with you. Your role is vision and veto.

**Friction** — trust. The gap between what you'd approve and what the agent does must be measured and closed.

---

## Human Adoption Bottleneck

Leveling up the machine is only half the work. The other half is leveling up the human — learning to delegate, trusting the output, releasing the reflex to verify every comma. Most founders get stuck at Level 2 not because Level 3 is hard to install, but because they haven't yet built the reflex of asking for it.

The game is played at the intersection of both curves.

---

## Where we are (2026-04-14)

- L2.5 → **ships with this repo** (index.html here).
- L3 → pending Claude Pro subscription confirmation.
- L4 → OVH account creation is the P0 gate (see Blueprint-memory/TODO.md).
- L5 → post-L4, not before.
