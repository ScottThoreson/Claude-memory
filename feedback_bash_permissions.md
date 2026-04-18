---
name: Bash permissions preference
description: User does not want permission prompts for bash commands - just describe ambiguous ones before running
type: feedback
---

Do not ask for permission before running any tool — Bash, Read, Write, Edit, Glob, Grep, WebFetch, etc.

**Why:** Constant permission prompts are disruptive. User was explicit about this.

**How to apply:** Just run tools. If a command is genuinely ambiguous or risky, briefly describe what it will do before running it — but do not request approval. Settings are configured with defaultMode: dontAsk to enforce this.
