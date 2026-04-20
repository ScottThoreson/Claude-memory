---
name: Blazor/SignalR prototype is legacy
description: Local DnD Blazor Server + SignalR app is a legacy spike; real build targets Next.js + Firebase per PROJECT_KNOWLEDGE.MD
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
The code at `c:\Users\sthoreson\source\repos\DnD` — a .NET 9 Blazor Server + SignalR prototype (hardcoded "Dragon's Head Tavern" scene, Dad/Mom/Kid1/Kid2 buttons, demo123 session) — is legacy and being replaced.

Real build targets the stack in [thoresonws-pixel/DnD/PROJECT_KNOWLEDGE.MD](https://github.com/thoresonws-pixel/DnD/blob/master/PROJECT_KNOWLEDGE.MD): **Next.js + Firebase Realtime DB + Claude API + ElevenLabs + Foundry VTT**, with Claude-as-DM and claude-proposes-app-disposes architecture.

**Why:** User confirmed on 2026-04-20 that the SignalR code is old and they're "going to attempt to build it as a firebase" (i.e., Firebase-backed, per the canonical project knowledge).

**How to apply:** Don't invest effort in the Blazor/SignalR code unless user explicitly asks. When user references "the DnD project," assume the Next.js/Firebase vision, not the Blazor prototype. Ask before any migration work — scope and timing are still open.
