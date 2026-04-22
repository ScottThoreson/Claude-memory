---
name: DnD MVP scope (post-pivot)
description: Scoped deliverables after the Scott-as-DM pivot; what's in the first playable loop vs. what's deferred
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
Following the 2026-04-21 pivot to Scott-as-DM (see `project_dnd_hybrid_workflow.md`), MVP scope is narrower than the original Claude-as-DM spec implied.

## In scope for the first playable session

1. **Foundry-direct player experience.** Players access Foundry in Chrome on phone/tablet — our `dnd-table-skin` module strips UI. Character sheet (Tidy 5e) auto-opens; chat available for voice input fallback. No custom phone app.
2. **DM page on Scott's laptop** at `/session/[id]/dm`. Wired to Foundry REST API (chat read/write, actor fetch). Manual active-speaker dropdown. Voice input via Web Speech API + Gamepad API. Narration textarea. Roll entry. "Copy Claude prompt" assembles `[NPC Exchange]` / `[Narration]` / `[Rules Query]` blocks.
3. **TV narration banner** via skin module. Fires on `!narrate <text>` chat content. Working end-to-end from POST via REST API.
4. **Claude.ai Pro Project** with instructions from `claude-project-instructions.md`. Scott pastes tagged blocks; Claude executes Foundry POSTs.
5. **Shared Razer mic + 1-2 passed controllers** as hardware.
6. **Delian Tomb** as the first adventure — small scope, good for proving the loop.

## Deferred (post-MVP or v2)

- **JRPG combat UI on TV** — reads Foundry combat state, renders menus, forwards controller input. ~2 days work; ship after MVP loop proven.
- **ElevenLabs voice synthesis** — NPC speech audio. ~$5-10/session. Ship after UX is stable.
- **Joy-Con / full gamepad polling on player phones** — Action button fallback is fine for MVP.
- **Voice identification (speaker ID)** — one-time 30s registration per family member, runtime speaker tagging. Manual override suffices for MVP.
- **Firebase-based session state sync** — mostly unnecessary now (Foundry owns state). Keep minimal — scene + narration only.
- **Claude API direct integration** — deliberately deferred until end. Wizard-of-Oz via Claude.ai chat until we're certain what we want.
- **Character creation flow** — use the standard Foundry drag-compendium workflow manually. Building a custom intake is deferred.
- **Campaign management / module ingestion pipeline** — original PROJECT_KNOWLEDGE.MD had elaborate seed-extraction. Under Scott-as-DM, that becomes Scott's prep process, not automation. Skip the extraction skills.
- **Promise-keeping / Chekhov audit** — manual under Scott-as-DM; skip the enforcement code.

## Hard scope flags

- **Don't rebuild what Foundry does.** Combat tracker, initiative, dice rolls, HP, actor data — Foundry. Reference, don't clone.
- **Don't add features that require paste-back from Claude.** Claude has API access; every new "Claude assist" flow should POST directly.
- **Prove the loop before polish.** One run-through of the Delian Tomb opening scene, end-to-end, with real family members, before adding any v2 features.

**Why this scope:** End-to-end validation beats feature count. Original v1 spec was too ambitious for the pivot; this scope is ship-able in 1-2 more sessions of dev.

**How to apply:**
- When considering any new feature, check: "Is this in MVP scope or deferred?" If deferred, note it and move on.
- If a feature would help prove the loop sooner, consider promoting from deferred to in-scope.
- Resist the urge to expand — the original PROJECT_KNOWLEDGE.MD is full of interesting directions that are tempting but off the critical path.
