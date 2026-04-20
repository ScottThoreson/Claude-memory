---
name: DnD MVP scope — narration first, mechanics later
description: For the first working loop, DM output is just prose narration; structured mechanical mutations (applyDamage, awardXP, addCondition) are deferred
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
Scope recommendation for the first playable loop (not yet formally approved by user as of 2026-04-20):

- **In scope for MVP:** player actions → DM narration prose → TV/phone rendering. The human-Claude wizard-of-oz writes natural-language responses into a `narration` RTDB slot.
- **Out of scope for MVP:** the full claude-proposes-app-disposes mutation system from PROJECT_KNOWLEDGE.MD. No `applyDamage`, `awardXP`, `useSpellSlot`, etc. yet. No typed character-state accessors. No combat round engine.
- Mechanical state (HP, conditions, XP, slots) gets layered in after the narration loop is proven at a real table for one session.

**Why:**
- PROJECT_KNOWLEDGE.MD itself flags the risk: *"prove the session-loop on a small hand-structured encounter before attempting full-module ingestion. Ingestion is the ambitious part; the runtime loop is the uncertain part. Validate the loop first."*
- Building the full tool-based mutation system before the loop works means potentially rebuilding it once we learn what actually matters at the table. Cheaper to learn first.
- Narration alone is enough to test: phone UI, TV display, realtime sync, session state, auth, character identity — most of the product surface area.

**How to apply:**
- When writing new code during MVP, resist scaffolding mutation tools until the user explicitly says "now layer in mechanics." If the user asks for HP or XP handling during MVP, push back once with the scope argument before building it.
- Keep the RTDB schema open to additions but don't pre-reserve slots for mechanics that aren't needed yet.
- When the loop is proven, re-read PROJECT_KNOWLEDGE.MD's "Claude proposes, the app disposes" section before designing the mutation layer — it specifies the tool surface (`getCharacter`, `applyDamage`, etc.) and the invariant that Claude never writes mechanical state directly.
