---
name: DnD Next.js skeleton build state (2026-04-20)
description: Current state of the DnD digital table Next.js skeleton, Firebase project, and local checkout
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
As of 2026-04-20 (work machine, user sthoreson):

- Local checkout of `thoresonws-pixel/DnD@master` lives at `c:\Users\sthoreson\source\repos\DnD-next`. The legacy Blazor/SignalR code at `c:\Users\sthoreson\source\repos\DnD` is left untouched.
- Stack: Next.js 16.2.4 + React 19.2.4 + Tailwind 4 + TypeScript 5. AGENTS.md hard rule: always read `node_modules/next/dist/docs/` before writing Next code — Next 16 has breaking changes (e.g. `params` / `searchParams` are now Promises and must be awaited).
- Firebase project `dnd-thoresonws` created. Web app registered. Realtime Database enabled (us-central1, test-mode rules expiring ~2026-05-20). Config lives in `.env.local` (gitignored).
- Scaffolded routes: `/` (role picker), `/session/[id]/player/[name]`, `/session/[id]/dm`, `/session/[id]/scott`. All four compile (HTTP 200 under `next dev`). Realtime sync works: phone action → RTDB → TV, verified by HTTP smoke test only — user has not yet browser-tested at time of writing.
- RTDB schema: `/sessions/{id}/{meta,scene,players,actions}`. Action entries are pushed with server timestamps.
- `firebase.json` + `.firebaserc` + `database.rules.json` staged but `firebase deploy --only database` has NOT been run (console test-mode rules still active).
- Nothing committed/pushed to `thoresonws-pixel/DnD` yet; user hasn't picked a hosting option.

**Why:** This is the snapshot to resume from. Work was paused to align on goals before locking in hosting, auth, and DM-output shape.

**How to apply:** When resuming, verify `npm run dev` still starts clean, confirm the Firebase project is still reachable, and check the user's pending decisions (hosting, auth method, MVP scope) before writing more code. Paths, schema, and versions in this memory are the ground truth for continuity; re-read current files if anything looks stale.
