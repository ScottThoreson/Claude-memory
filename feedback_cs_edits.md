---
name: C# code edit discipline
description: Don't speculatively edit .cs files when user is asking questions - clarify first
type: feedback
---

When the user asks a question about C# code, do not edit files unless the fix is unambiguous. Describe the proposed change first and wait for confirmation.

**Why:** User wants code control. Edits during Q&A feel like getting ahead of yourself.

**How to apply:** Clear bug fix or compile error with an obvious solution → just fix it. Question, investigation, or multi-step change → explain what you'd change and why before touching any .cs file.
