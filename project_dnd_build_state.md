---
name: DnD build state (2026-04-21 EOD)
description: Comprehensive snapshot of the DnD digital table build at end of the 2026-04-21 session
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
**Session of 2026-04-21 was huge.** Design locked in, most infrastructure built, first tests green. User went to bed after "sync all".

## Current state

**Canonical repo:** `thoresonws-pixel/DnD@master` — commit `b674c90` has all the code. PROJECT_KNOWLEDGE.MD @ commit `6966724` (reflects the big pivot + hardware plan + voice ID v2).

**Local checkout on work machine (sthoreson user):** `c:\Users\sthoreson\source\repos\DnD-next`

**Foundry VTT v14.360** running locally with world "Delian Tomb Test". D&D 5e 5.3.1 system. Running at `http://localhost:30000` and LAN-reachable at `http://192.168.1.167:30000`.

**Foundry project on foundryrestapi.com relay** paired, 5000 calls/mo free tier. Client ID `fvtt_0b877c160c8b8a36`. REST API + key lives in `.env.local`; same values are referenced in `claude-project-instructions.md` for the Claude.ai Project setup.

**Firebase project `dnd-thoresonws`** still live but less central now (Foundry is source of truth for game state).

## The big pivot (2026-04-21)

**Scott is DM; Claude assists.** Original PROJECT_KNOWLEDGE.MD said "Claude is DM, Scott plays player-blind" — that changed mid-session. See commit `f06aa04` on master. Architecture now:
- **Foundry** = engine for all game state (actors, combat, dice, rolls, HP, scenes, maps)
- **Our Next.js DM page** = Scott's companion tool, runs in browser on his laptop alongside Foundry GM view
- **Our `dnd-table-skin` Foundry module** = UI skin for TV Display + player phones
- **Claude.ai Project** (Pro subscription) = NPC voice + descriptions + rules lookups. Claude has Foundry REST API credentials in its Project instructions, uses Python code-execution to POST responses directly to Foundry chat. No paste-back required.

## What got built today

- **`dnd-table-skin` Foundry module** at `foundry-modules/dnd-table-skin/` in the repo (+ installed at `C:\Users\sthoreson\AppData\Local\FoundryVTT\Data\modules\dnd-table-skin`)
  - Strips Foundry UI by role: Player role gets clean sheet-focused view; TV Display user gets scene-only fullscreen
  - **Narration banner** on TV: typewriter animation, 15s auto-dismiss, triggered by `!narrate <text>` chat prefix or speaker alias "Narrator". **Works** — tested via REST API → banner fires on TV ✅
  - **Combat mode**: top banner "YOUR TURN" (pulsing gold) driven by Foundry `combatStart`/`updateCombat` hooks
  - **Leader arrow pad**: injected when `tactical + leader` flags set via `!tactical on` / `!leader <id>` GM chat commands
  - **Player ACTION button**: slide-up dialog on phones without a controller
  - **Auto-open character sheet** for Player-role users on mobile
- **Next.js DM companion page** at `/session/[id]/dm` — full layout with active speaker, active NPC, voice input (Web Speech API + Gamepad API Start button), player feed, narration direct, roll entry, copy-context-to-Claude prompt builder. **Compiles 200, needs real browser testing.**
- **API proxies** for Foundry REST API: `/api/foundry/chat` (GET list, POST send), `/api/foundry/actors` (list), `/api/foundry/actors/[uuid]` (specific).
- **Claude Project instructions** drafted at `claude-project-instructions.md` in the repo — ready for Scott to paste into a Claude.ai Pro Project.
- **Foundry content**: Thorin actor exists (level 3 Dwarf Fighter, stat block via REST API update; items need to be drag-added from compendium). TV Display user exists.
- **Foundry modules enabled in world:** Tidy 5e Sheets, Foundry REST API, Theatre Inserts, Dice So Nice!, Mobile Improvements, Custom CSS (broken on v14 — left disabled), libWrapper, PocketScroll Foundry Companion (installed but user rejected paid sub), TouchVTT.

## Hardware plan (locked)

- **Scott's laptop** = central hub. Runs Foundry GM + DM page + Bluetooth controllers + USB Razer mic.
- **1-2 full-size controllers** passed around (8BitDo Pro 2 ~$50 recommended, or Xbox ~$60). JRPG-style.
- **Razer USB mic** at table center — single shared mic, wired (doesn't eat BT slots).
- **Joy-Cons rejected** for primary input (felt not-epic) but can serve as fallback.
- **Family Switches exist** — used for Joy-Cons if we revisit, also their TVs are candidates.
- **Phones optional** — anyone who wants character sheet handy opens Foundry URL in Chrome.

## Not built / open items

- **JRPG combat TV UI** (scoped, ~2 days of work — reads Foundry combat state, renders menu, forwards controller input)
- **ElevenLabs voice integration** for NPC speech synthesis
- **Joy-Con / full gamepad polling** for Action/menu navigation on player phones
- **Voice ID v2** (browser-side speaker embedding) — planned as follow-up feature
- **NPCs in Foundry** — only Thorin as player character exists. Need Barkeep + other test NPCs with biography `[personality]` / `[knowledge-*]` tags
- **Scenes/maps** — using default Foundry splash; need a real Delian Tomb scene
- **Real end-to-end playtest** — hasn't happened yet. DM page not exercised in browser.

**Why:** End-of-session snapshot so future-me doesn't have to re-derive state from scratch.

**How to apply:** At start of next session, verify `npm run dev` still starts clean in `DnD-next`, Foundry is still reachable + REST API paired, and the big outstanding item to drive toward is a real self-playtest of the DM page + skin module + Claude Project together.
