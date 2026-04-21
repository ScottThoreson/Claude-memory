---
name: Code edit discipline — describe before editing
description: Don't speculatively edit code when the user is thinking out loud or asking questions. Describe the proposed change and wait for confirmation.
type: feedback
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
When the user makes a design observation, asks a question, or expresses a preference, do NOT immediately edit files — no matter the language (C#, TypeScript, React, config, etc.). Describe what you'd change, where, and why, and wait for a go-ahead.

**Why:**
- User wants code control. Unsolicited edits during discussion feel like getting ahead of yourself.
- Originally framed around .cs files; generalized 2026-04-20 after I jumped straight into editing Next.js / TypeScript files when the user was thinking aloud about placeholder names. User's words: *"you need to do a better job of not just changing stuff and instead asking for input."*

**How to apply:**
- Clear bug fix, compile error, or explicit instruction ("rename this to X") → just do it.
- Design observation, question, preference, or "maybe we could" → describe the change, name the files, name the tradeoff, then wait.
- When unsure which bucket the user's message falls into, default to describing-first. Cost of pausing is low; cost of wrong edit is a revert and a lost trust point.
- Applies to ALL code surfaces, not just C#.
