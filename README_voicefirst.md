# README_voicefirst.md
## The Voice-First Protocol / Le Protocole Voice-First

**Enter-Game · v1.0 · April 2026**

---

> Voice is not dictation. Voice is the bridge between internal cognition and external execution.
> This document makes the voice protocol reproducible for anyone who wants to use it.
>
> *La voix n'est pas de la dictée. La voix est le pont entre la cognition interne et l'exécution externe.
> Ce document rend le protocole vocal reproductible pour quiconque veut l'utiliser.*

---

## TWO READING MODES / DEUX MODES DE LECTURE

| 🛠️ **DEV BRANCH** | 🧭 **NON-DEV BRANCH** |
|---|---|
| AssemblyAI/Whisper integration, n8n dispatch nodes, webhook architecture, biometric voice | "Think out loud, the agent handles the rest" — the 5-step protocol |

---

## WHY VOICE? / POURQUOI LA VOIX ?

### [NON-DEV]

Most people use voice-to-text as a faster keyboard. That's a fraction of its actual power.

When you speak, you think differently. Less filtered. More associative. You catch connections you'd miss while typing. You express uncertainty more naturally ("I think maybe we should... actually no, wait..."). That uncertainty is data. The agent captures it.

**The research signal:** Voice interactions produce 3–5x more contextual information per minute than typed prompts. Most of that extra information is in the texture — hesitation, course-correction, implicit assumptions — and it makes the agent's outputs dramatically more aligned.

**The practical reality:** You're not always at a keyboard. Walking to a meeting, commuting, making coffee, doing the dishes — these are dead time if your interface requires a screen. They become productive if your interface is your voice.

Voice-first doesn't mean "only voice." It means voice is the primary cognitive interface, and text is the secondary delivery format.

---

### [DEV]

**The gap identified in POWERUSER-FUTURE.md (2026):**
> "Voice pipeline → dispatch async is not yet formalized. The chain voice → context engineering → dispatch AI + async human hasn't been documented as a systematic protocol. When the user speaks out loud, how the context is structured, how dispatch triggers, how feedback returns by voice — it's implicit, not formalized. Impact: not reproducible, not teachable, not integrable into Enter-Game."

This document closes that gap.

**Market context:**
- $2.1B invested in voice AI in 2024 (7x from 2022)
- 87.5% of builders actively building voice agents (Voice Agent Report 2026)
- Kardome / AssemblyAI contextual awareness stack: speaker biometrics + acoustic location + command vs ambient detection + conversational memory
- **The unresolved gap**: nobody has documented the complete voice → context → orchestration → async dispatch → feedback loop

---

## THE 5-STEP PROTOCOL / LE PROTOCOLE EN 5 ÉTAPES

```
STEP 1: INPUT        Voice captured
STEP 2: STRUCTURE    Voice → structured context
STEP 3: DISPATCH     Context → routing decision
STEP 4: EXECUTION    Agent / human executes
STEP 5: FEEDBACK     Result returned to human
```

---

## STEP 1 — VOICE INPUT / INPUT VOCAL

### [NON-DEV]

You speak. That's it. But there are two modes:

**Cognitive mode:** Thinking out loud. "I've been wondering about the onboarding flow... maybe we should split it into three steps... actually the problem is the user doesn't know what they're signing up for yet..."
→ Produces rich context. Agent captures the reasoning, not just the conclusion.

**Command mode:** Direct instruction. "Go: write the API spec for the onboarding flow."
→ Produces clear task brief. Agent executes immediately.

The protocol supports both. The key is knowing which mode you're in.

---

### [DEV] Technical Implementation

**Transcription options:**
```
Option A (local):     OpenAI Whisper (self-hosted, free, latency ~0.5–2s)
Option B (cloud):     AssemblyAI (99%+ accuracy, real-time streaming, $0.37/hr)
Option C (device):    iOS/macOS native speech recognition (offline, no API cost)
Option D (native):    Claude iOS app built-in voice (no setup, limited control)
```

**Recommended stack for production:**
```
Mobile trigger → AssemblyAI streaming → n8n webhook → context structuring
```

**AssemblyAI realtime setup:**
```python
import assemblyai as aai

aai.settings.api_key = "YOUR_KEY"

def on_data(transcript: aai.RealtimeTranscript):
    if not transcript.text:
        return
    if isinstance(transcript, aai.RealtimeFinalTranscript):
        process_voice_input(transcript.text)

transcriber = aai.RealtimeTranscriber(
    sample_rate=16_000,
    on_data=on_data,
    on_error=lambda e: print(f"Error: {e}")
)
transcriber.connect()

# Stream audio from microphone
```

**Voice mode detection (automatic):**
```python
def detect_voice_mode(transcript: str) -> str:
    command_triggers = ["go:", "deploy:", "commit", "status", "interview me on"]
    if any(transcript.lower().startswith(t) for t in command_triggers):
        return "command"
    if len(transcript.split()) > 15:  # longer utterances = thinking out loud
        return "cognitive"
    return "command"  # default to command for short utterances
```

---

## STEP 2 — CONTEXT STRUCTURING / STRUCTURATION DU CONTEXTE

### [NON-DEV]

Raw voice → structured brief. This is the step that converts your words into something the agent can act on without ambiguity.

**What the structuring does:**
- Extracts the task (what needs doing)
- Identifies the project (which one)
- Extracts constraints (time, budget, preference)
- Captures context clues (reasoning, uncertainty, implicit info)
- Generates metadata (timestamp, voice mode, priority)

**Example:**
```
Raw voice: "Okay so I'm thinking about the onboarding, it's too long right now,
           people are dropping off, maybe we cut the email verification step
           or at least defer it? Figure out what's standard."

Structured:
  Task: Research best practices for email verification timing in onboarding flows
  Project: EasyRead
  Constraint: Looking for industry standard, not inventing
  Context: Current onboarding has drop-off — verification step suspected cause
  Mode: research → dispatch to Researcher agent
  Priority: medium
```

---

### [DEV] Structuring Agent

**System prompt:**
```
You are the Voice Context Structurer in the Enter-Game pipeline.
Your role: convert a voice transcription into a structured task brief.

Input: raw transcription
Output: JSON task brief

Rules:
- Extract explicit tasks AND implicit requests (thinking out loud may contain tasks)
- Preserve uncertainty markers — they're context ("maybe", "I think", "unless")
- If multiple tasks detected: output as array, maintain sequence
- Assign project based on known project list from CONTEXT.md
- Assign dispatch type: AI_immediate | AI_async | human_async | clarification_needed

Output schema:
{
  "tasks": [
    {
      "description": "...",
      "project": "...",
      "constraints": [...],
      "context": "...",
      "dispatch": "AI_immediate | AI_async | human_async | clarification_needed",
      "priority": "high | medium | low",
      "voice_mode": "command | cognitive"
    }
  ],
  "raw_input_preserved": "...",
  "timestamp": "ISO8601"
}
```

---

## STEP 3 — DISPATCH / DISPATCH

### [NON-DEV]

The routing decision: what handles this task, and how fast?

**Three dispatch channels:**

**Channel 1 — AI Immediate:** The agent starts right now. Used for: code, research, analysis, writing. Result in seconds to minutes.

**Channel 2 — AI Async:** The agent queues the task. Used for: long-running jobs (training, large generation), tasks that need to run while you do something else. Result in minutes to hours. Notification when done.

**Channel 3 — Human Async:** The task goes to a human specialist (Fiverr, Contra, your network). Used for: design, legal, specialized domain work, physical tasks. Result in hours to days.

The key principle: **dispatch to the fastest capable channel**. Never use a human for something AI can do well. Never use AI immediate for something that can safely wait.

---

### [DEV] Dispatch Logic

**Decision tree:**
```python
def dispatch(task: dict) -> str:
    
    # Human-required tasks
    if task["requires_physical_action"]:
        return "human_async"
    if task["requires_specialized_domain"] and not ai_has_domain_coverage(task):
        return "human_async"
    if task["estimated_cost_usd"] > budget_threshold:
        return "human_async"  # escalate to human for approval
    
    # AI async tasks
    if task["estimated_duration_minutes"] > 15:
        return "AI_async"
    if task["can_run_in_background"] and task["priority"] != "high":
        return "AI_async"
    
    # AI immediate (default for most tasks)
    return "AI_immediate"
```

**Dispatch routing table:**
```
Task type                      Dispatch          SLA
─────────────────────────────────────────────────────
Code writing/review            AI_immediate      < 2 min
Research                       AI_immediate      < 5 min
Long-form content              AI_async          < 30 min
ML training job                AI_async          hours
Design work                    human_async       1–3 days
Legal review                   human_async       days
Complex analysis               AI_immediate      < 10 min
Deployment (with confirmation) AI_immediate +    confirm first
                               human confirm
```

**n8n routing node:**
```
Input: structured task JSON
→ Switch node: dispatch type
   ├── AI_immediate → call AI agent → return result inline
   ├── AI_async → queue job → send confirmation → webhook on completion
   └── human_async → create task card (Notion/Linear/Fiverr) → notify human
```

---

## STEP 4 — EXECUTION / EXÉCUTION

### [NON-DEV]

You've dispatched the task. Now you do something else.

This is the core unlock of voice-first: **decoupled execution**. You speak a task into existence, and the system handles it while you walk, drive, sleep, or work on something else.

For AI immediate: result is ready before you put your phone away.
For AI async: you get a notification when it's done.
For human async: it's in a queue, you'll hear back.

You don't need to wait. You don't need to monitor. You move.

---

### [DEV] Async Execution Patterns

**AI async with callback:**
```python
import asyncio
from typing import Callable

async def execute_async_task(task: dict, callback: Callable):
    """Execute a long-running task and call back when done."""
    result = await ai_agent.execute(task)
    await callback(result, task["user_id"])

async def notify_user(result: dict, user_id: str):
    """Send notification back to user."""
    if result["delivery_channel"] == "voice":
        await send_voice_notification(user_id, result["summary"])
    elif result["delivery_channel"] == "push":
        await send_push_notification(user_id, result["summary"])
```

**Human async dispatch (Notion integration):**
```python
def create_human_task(task: dict, assignee: str):
    notion.pages.create(
        parent={"database_id": TASKS_DB_ID},
        properties={
            "Task": {"title": [{"text": {"content": task["description"]}}]},
            "Project": {"select": {"name": task["project"]}},
            "Assignee": {"people": [{"id": assignee}]},
            "Context": {"rich_text": [{"text": {"content": task["context"]}}]},
            "Due": {"date": {"start": task["deadline"]}},
            "Source": {"select": {"name": "voice_dispatch"}}
        }
    )
```

---

## STEP 5 — FEEDBACK / RETOUR

### [NON-DEV]

The result comes back. How it comes back is a choice.

**Voice feedback:** A voice message summarizes the result. Best for: brief status updates, confirmations, non-technical results. You don't need to look at a screen.

**Push notification:** A short notification with result summary. Best for: async tasks completing while you're doing something else.

**Inline (text):** Full result delivered in the chat interface. Best for: code, documents, structured outputs you'll want to edit.

**The rule:** match feedback channel to task type. Don't send a 400-line code diff as a voice message.

---

### [DEV] Feedback Channel Routing

```python
def route_feedback(result: dict, task: dict) -> str:
    """Route result to appropriate feedback channel."""
    
    if result["type"] == "code" or result["type"] == "document":
        return "inline_text"
    
    if task["dispatch"] == "AI_async" or task["dispatch"] == "human_async":
        return "push_notification"
    
    if task["voice_mode"] == "cognitive":
        # User was thinking out loud — brief voice summary appropriate
        return "voice_summary"
    
    return "inline_text"  # default

def generate_voice_summary(result: dict) -> str:
    """Generate a < 30 second spoken summary of the result."""
    prompt = f"""
    Summarize this result in one spoken sentence (< 20 words).
    Result: {result['content'][:500]}
    Format: "[action completed]. [1-line outcome]. Next: [if applicable]."
    """
    return llm.complete(prompt)
```

**TTS for voice feedback:**
```python
# Using ElevenLabs or system TTS
def speak(text: str, voice_id: str = "default"):
    audio = elevenlabs.generate(text=text, voice=voice_id, model="eleven_monolingual_v1")
    play(audio)
```

---

## MAKING IT REPRODUCIBLE / RENDRE ÇA REPRODUCTIBLE

### [NON-DEV] Your Setup in 4 Steps

**Step 1:** Choose your transcription tool (Claude mobile app built-in for simple setup, or AssemblyAI for production).

**Step 2:** Set up your dispatch vocabulary — learn the command triggers your system responds to:
```
"Go: [task]"         → AI immediate
"Queue: [task]"      → AI async
"Ask [name]: [task]" → human async
"Interview me on [X]" → 5–8 questions before executing
```

**Step 3:** Run the first voice session. Say: *"Go: read my CONTEXT.md and confirm my active projects."*

**Step 4:** Practice cognitive mode once. Walk somewhere and narrate your thinking on a current problem for 2 minutes. Review what the structuring agent extracted. Adjust your narration style based on what was captured vs missed.

---

### [DEV] Minimal Reproducible Setup

```bash
# Dependencies
pip install assemblyai openai python-dotenv requests

# Environment
ASSEMBLYAI_API_KEY=your_key
OPENAI_API_KEY=your_key
GITHUB_TOKEN=your_token
MEMORY_REPO=your-username/your-memory-repo

# Run
python voice_gateway.py
```

**voice_gateway.py skeleton:**
```python
"""
Minimal Enter-Game voice gateway.
Captures voice → structures context → dispatches → returns feedback.
"""
import assemblyai as aai
from context_structurer import structure_input
from dispatcher import dispatch_task
from feedback import route_feedback

def process_voice_input(transcript: str):
    # Step 2: Structure
    structured = structure_input(transcript)
    
    # Step 3: Dispatch
    for task in structured["tasks"]:
        result = dispatch_task(task)
        
        # Step 5: Feedback
        feedback_channel = route_feedback(result, task)
        deliver_feedback(result, feedback_channel)

# Step 1: Input
transcriber = aai.RealtimeTranscriber(
    sample_rate=16_000,
    on_data=lambda t: process_voice_input(t.text) if isinstance(t, aai.RealtimeFinalTranscript) else None
)
transcriber.connect()
```

---

## THE TWO MODES / LES DEUX MODES

Enter-Game voice-first works in two modes. You can operate in either.

| | **Voice-First** | **Text-First** |
|---|---|---|
| Primary interface | Voice (earbuds, phone) | Keyboard (desktop, laptop) |
| Best for | Mobile, commute, hands-busy | Deep work, code review, documents |
| Context quality | Richer (less filtered thinking) | Precise (more structured input) |
| Dispatch speed | Faster to initiate | Faster to review |
| Protocol used | Same | Same |

The underlying protocol — context load → batch → dispatch → feedback — is identical. Only the input and feedback channels differ.

---

*Enter-Game · README_voicefirst.md · v1.0 · April 2026*
