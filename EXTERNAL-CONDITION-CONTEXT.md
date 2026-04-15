# External Condition Context
## Version 1.0 · April 2026
## Role: Brain Chip Interface Layer

---

## Purpose

This file describes the current state of the external interface between Yoan's brain (vision, thought, direction) and the world (web, AI systems, execution layer).

It is a **living document**. As technology evolves — better hardware, lower latency, higher bandwidth, eventual neural interfaces — this file gets updated to reflect the new reality.

---

## Current Interface: Headset (2026)

**Device type:** Audio headset (voice input / audio output)
**Connection:** Wireless / Bluetooth
**Brain connection:** None — indirect. Voice is the bridge.
**Latency:** ~100–300ms round trip (speech recognition + TTS response)
**Bandwidth:** Low — sequential, voice-only. One thought at a time.

### What it does
- Captures voice input from Yoan (thoughts → words → text)
- Delivers audio output back (text → speech → ears)
- Enables hands-free, mobile-first operation
- Works while commuting, walking, in transit

### What it cannot do (yet)
- No direct neural signal reading
- No parallel thought streams
- No ambient sensing
- No haptic or visual feedback layer
- No passive always-on context capture

---

## Role in the System

The headset is the **external chip** — the closest available solution today to a brain-computer interface.

It sits at **Stage 2** of the Pipeline:

```
Grain (brain) → Headset Interface → Claude → blueprint-memory → Action
```

It is the **bottleneck** of the current pipeline. Every improvement in interface technology directly improves the throughput of the entire system.

---

## Evolution Roadmap

| Year | Interface | Bandwidth | Latency | Notes |
|------|-----------|-----------|---------|-------|
| 2026 | Headset (audio) | Low | 100–300ms | Current state |
| 2027 | Enhanced headset + eye tracking | Medium | 50–100ms | Projected |
| 2028+ | Neural interface (read-only) | High | <10ms | Speculative |
| 2030+ | Bidirectional BCI | Very high | <1ms | Long-term vision |

---

## Design Principles for This Interface

- **Voice-first always** — every system built around Yoan must work via voice
- **Concise responses** — short, actionable, no fluff. Headset = limited audio bandwidth.
- **Async-friendly** — Yoan may be moving. Systems must handle interruptions gracefully.
- **No screen dependency** — core workflows must function without looking at a screen

---

## Update Protocol

When this file needs updating:
1. Yoan says "update brain chip context" or "update external condition"
2. Claude drafts the new version with version number and date
3. File gets committed to `blueprint-memory` and uploaded to `enter-game` repo

---

*Last updated: April 14, 2026 · Yoan Maisonneuve · openClaude project*
