---
name: Laptop memory sync setup
description: Reminder to set up Claude memory sync on laptop
type: project
originSessionId: 7c4670e2-39db-4d84-8d81-ec1d5798b206
---
Still need to run on laptop:

1. `git clone https://github.com/ScottThoreson/Claude-memory.git "C:/Users/12146/.claude/projects/C--Users-12146/memory"`
2. Copy `C:/Users/12146/.claude/settings.json` (the Stop hook for auto-push) to the same path on the laptop.

**Why:** Desktop is fully set up. Laptop needs the clone + settings.json to join the same GitHub-backed memory system.

**How to apply:** Once done, both machines will auto-sync memories to ScottThoreson/Claude-memory on session end.
