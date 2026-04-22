---
name: DnD hybrid Scott-DM / Claude-assist workflow
description: The end-state play workflow — Scott DMs, Claude.ai Project handles NPCs via direct Foundry REST API calls
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
The end-state session flow is a **hybrid**: Scott is the DM (pacing, adjudication, rolls), Claude.ai is an assistant that handles NPC voices, scene imagery, and rules lookups — and *executes Foundry API calls itself* rather than round-tripping text via copy-paste.

**Enabling capability:** Claude.ai Pro's Analysis tool can run Python and make HTTP requests. Given Foundry REST API credentials in the Project instructions, Claude writes and POSTs NPC responses/narration directly.

## The roundtrip at runtime

1. **Event at table:** player says "Thorin asks the barkeep what the notice says" (voice into shared Razer mic, transcribed by Web Speech API on the DM page).
2. **Scott confirms transcription,** commits as "Thorin", which posts to Foundry chat (normal chat message).
3. **DM page "Copy Claude prompt"** assembles a tagged block including the active NPC's profile + the player's message:
   ```
   [NPC Exchange]
   Active NPC: Barkeep
   Personality: ...
   Knowledge-open: ...
   Knowledge-guarded: ...
   Knowledge-secret (never reveal): ...
   Player (Thorin): "What do you know about the notice?"
   ```
4. **Scott pastes into Claude.ai Project** chat. The Project has pre-loaded system instructions (see `claude-project-instructions.md` in the repo) telling Claude:
   - Generate a 1-3 sentence in-character reply.
   - POST it to Foundry chat with `requests.post("https://foundryrestapi.com/chat?clientId=<id>", headers={"x-api-key": "<key>"}, json={"content": "Barkeep: <line>"})`.
   - Confirm in chat.
5. **Foundry receives the POST,** Theatre Inserts fires (if Scott has "Speak as → Barkeep" selected on GM view), TV banner animates.
6. **Scott doesn't paste anything back.** Just confirms visually on the TV and moves on.

## Tag conventions (what triggers what in the Project instructions)

- `[NPC Exchange]` — in-character NPC response, POST with NPC name prefix in content
- `[Narration]` — atmospheric prose, POST with `!narrate` prefix to fire banner
- `[Rules Query or Assist]` — stays in chat, no POST
- `[Gamestate]` — broader session context, Claude acknowledges but doesn't POST

## Known limitations

- **Foundry REST API POST `/chat` ignores `speaker` and `flags` body fields.** Our skin module intercepts `!narrate` via `preCreateChatMessage` hook so speaker is set to "Narrator" correctly. For NPC attribution, the Claude prompt puts the NPC name in the content prefix (e.g. `"Barkeep: <line>"`). For proper Theatre Inserts portrait animation, Scott sets the "Speak as" dropdown on the GM view to the specific NPC actor before letting Claude POST — Theatre Inserts picks that up regardless of who authored the HTTP request.
- **Claude.ai Pro required** — the Analysis (code-execution) tool isn't in the free tier.
- **Claude chat context is per-conversation** — Project persists instructions across chats, but specific NPC voice memory within a single conversation resets on new chats. Keep long sessions in one Claude chat thread for voice consistency.

**Why this workflow won:**
- Scott retains creative authority (pacing, adjudication)
- Claude does what it's best at (consistent NPC voice, on-demand prose)
- No clunky paste-back step — POST is automated
- Foundry stays the source of truth for mechanics/state
- Costs ~$1-2/session for Claude.ai Pro usage vs. API-level spend

**How to apply:**
- Any future DM-page feature should produce **tagged context blocks** Claude can act on unambiguously.
- Don't rebuild functionality that Foundry already does (combat tracker, dice rolls, HP tracking) — reference Foundry instead.
- When designing new features, ask: "Does this require a paste-back step? If yes, can Claude do it via API instead?"
- Starting file for the Claude Project instructions: `claude-project-instructions.md` in the repo.
