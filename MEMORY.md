# Claude Bootstrap Index

Start every new conversation by reading this file.

## How to Bootstrap
1. Read: https://github.com/ScottThoreson/Claude-memory/blob/main/MEMORY.md
2. Load tokens from: C:\Users\12146\.claude-tokens.env
3. Navigate to project-specific memory (listed below)

## Token Location
C:\Users\12146\.claude-tokens.env (NOT in GitHub)

## Active Projects

### DnD Digital Table
- Account: thoresonws-pixel
- Repo: https://github.com/thoresonws-pixel/DnD
- Memory: https://github.com/thoresonws-pixel/DnD/blob/master/PROJECT_KNOWLEDGE.MD

### CC17
- Account: ScottThoreson
- Repo: https://github.com/ScottThoreson/CC17

## Personal Context
- Name: Scott Thoreson
- Expertise: C#, ASP.NET Core
- Style: Direct, action-oriented

## Preferences
- [Laptop setup](project_laptop_setup.md)
- [Bash permissions](feedback_bash_permissions.md)
- [C# edits](feedback_cs_edits.md)

## DnD Project Notes
- [Blazor/SignalR is legacy](project_blazor_is_legacy.md) — real build targets Next.js + Firebase per PROJECT_KNOWLEDGE.MD
- [Build state 2026-04-20](project_dnd_build_state.md) — Next.js 16 skeleton scaffolded at `DnD-next`; Firebase `dnd-thoresonws` live; nothing pushed yet
- [Wizard-of-Oz testing](project_dnd_wizard_of_oz_testing.md) — Claude Code simulates DM via direct RTDB writes; no Anthropic spend during testing
- [Auth + persistence design](project_dnd_auth_and_persistence.md) — per-user Firebase Auth, players keyed by auth.uid, characters persist across sessions
- [Hosting open](project_dnd_hosting_open.md) — Vercel vs Pages+Functions vs Pages+laptop; decision deferred
- [MVP scope](project_dnd_mvp_scope.md) — narration-first; defer structured mechanical mutations until loop is proven
- [Firebase coordinates](reference_dnd_firebase.md) — project ID, RTDB URL, repo, local paths
