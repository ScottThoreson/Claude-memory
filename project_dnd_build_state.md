---
name: DnD build state (2026-04-23 EOD)
description: End-of-session snapshot — what's built, what's tested, what's next
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
## Current state (end of 2026-04-23 session)

**Canonical repo:** `thoresonws-pixel/DnD@master`. Relevant commits since the 2026-04-21 snapshot:
- `3f361cf` — skills cleanup (deleted 8 obsolete specs, rewrote 4 for hybrid)
- `ec4ff81` — added Brena/Pell/Garrin + Owlbear/Spider/Skeleton to `prep/delian-tomb-npcs.md`
- `8ccb587` — `scripts/create-npcs.mjs` (batch-create NPCs via REST API)
- `59e58c4` — `prep/macros/` (6 scene macros: narrate, combat-start, arrow-trap, boss-skarvax-phase2, secret-door-reveal, scene-transition-fade)

**Local Next.js repo at `c:\Users\sthoreson\source\repos\DnD-next`:** clean, no uncommitted changes.

**Foundry world "Delian Tomb Test":**
- Actors created via REST API: Thorin (player character, updated yesterday), plus 12 new NPCs/monsters — Elder Marta, Barkeep Dain, Brena, Old Pell, Merchant Hollis, Garrin, Skarvax, Elric, Owlbear, Giant Spider, Skeleton, Goblin. Each has biography tags (`[personality]`, `[knowledge-open/guarded/secret]`) ready for Claude to parse.
- Scenes created via REST API (bare, no background): "Hollowmere Village", "Forest Path", "Delian Tomb Interior".
- **Hollowmere Village** has 2 Minute Tabletop's Coastal Town night map loaded. No walls yet. No tokens placed yet.
- Foundry modules active: Tidy 5e Sheets, Foundry REST API, Theatre Inserts, Dice So Nice!, Mobile Improvements, Custom CSS (broken on v14, disabled), libWrapper, PocketScroll Foundry Companion, TouchVTT, Monk's Active Tile Triggers, Sequencer, JB2A Free. Plus custom `dnd-table-skin`.
- `narrate` macro installed, drag to hotbar working; narration banner fires on TV ✓ end-to-end validated.

**DM page** at `http://localhost:3000/session/demo/dm` browser-tested. All panels work. Active NPC dropdown populates from Foundry actors. Voice input / mic / transcription works (pending real playtest).

## Notable decisions today

- **Rejected Baileywiki direct subscription** — their new store is primarily DungeonDraft asset packs + AI credits, not pre-built Foundry scenes. Not the right tool for "I just want a map and some houses."
- **Rejected Draw Steel switch** — the free Delian Tomb module on Foundry is for MCDM's Draw Steel system, not D&D 5e. Different rules, would require rebuilding Thorin + learning a new system. Family already knows 5e; staying.
- **Still undecided on Delian Tomb's final village map** — Coastal Town works as placeholder. May hunt 2MT or Dyson for something smaller, may stick with what's there.

## What's next (open for tomorrow)

1. **Build out the Tomb Interior scene** — needs a map (Dyson Logos free dungeons are the path), walls, lighting, token placement. This is the only scene that actually needs the heavy wall-drawing work.
2. **Drop NPC tokens** onto Hollowmere Village scene so the social scene feels populated (~10 min).
3. **Install remaining macros** as needed — probably `combat-start-banner` next, defer the others until their specific scenes exist.
4. **Forest Path scene** — either AI-generate an atmospheric image or grab from r/battlemaps.
5. **Claude.ai Pro Project setup** — user still hasn't created the Project; `claude-project-instructions.md` in the repo is the starting template. Needed before any real NPC dialogue can run through Claude.

## Known things deferred per MVP scope

- JRPG combat UI on TV — after loop proven
- ElevenLabs voice — after UX stable
- Joy-Con input — after core working
- Voice ID v2 — manual speaker dropdown suffices
- Claude API direct integration — Wizard-of-Oz via Claude.ai only for now

**Why:** All decisions + state captured so next session can resume without re-deriving.

**How to apply:** At next session start, check that dev server still runs, Foundry is reachable, REST API pairing is still valid (commonly needs quick re-pair after relaunch). The biggest outstanding artifact is the Tomb Interior scene — focus there first if we want an end-to-end playtest.
