---
name: DnD Wizard-of-Oz testing strategy
description: Human-Claude (Claude Code) simulates the DM brain by writing directly to Firebase during testing — no Anthropic API spend until the loop is proven
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
During the pre-production phase, the "DM brain" is played by Claude Code (me, in the user's chat), NOT by Claude API calls. I read/write RTDB via the REST API at `https://dnd-thoresonws-default-rtdb.firebaseio.com/<path>.json` using bash + curl. The client app is identical to production — it subscribes to RTDB and renders whatever shows up there; it doesn't know whether a human-Claude or API-Claude produced the narration.

**Why:** Two reasons.
1. Avoid burning Anthropic credits while iterating on UI, schema, and session loop. Per PROJECT_KNOWLEDGE.MD's own v1 scope flag: *"prove the session-loop on a small hand-structured encounter before attempting full-module ingestion."*
2. De-risks the hosting decision — no server-side Claude proxy needed during testing, so GitHub Pages is viable for this phase. We only need to pick a server (Vercel / Firebase Cloud Functions on Blaze) when we're ready to wire the real Claude API.

**How to apply:**
- When the user asks me to "respond as DM," curl the relevant RTDB path, read the latest player actions, decide a narrative response, and PATCH/POST back. Treat my output as if it were Claude-API output — same shape, same contract.
- DM output lives in its own slot under the session (separate from player actions) so the client can render it distinctly. Schema TBD — not yet added to `lib/types.ts` or the UI.
- The swap-out to real Claude API later is a server-side change only: the route that currently doesn't exist gets added, and it writes to the same RTDB slot. Zero client-side refactor if the schema is stable.
- Keep RTDB rules permissive enough during this phase that unauthenticated curls from me work. Lock down only after the real API server is introduced.
