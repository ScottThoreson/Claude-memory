---
name: ScriptWright — safety-first LLM macro generator for Foundry
description: Free Foundry module that safely runs Claude-generated macros against the world — key tool for content-build phase
type: reference
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
**ScriptWright** — [scriptwright.com](https://scriptwright.com/) — free Foundry VTT module that wraps LLM-generated macro execution with safety validation. Works with Claude.

- Supports AI models: **Claude**, Gemini, others.
- Validates generated code before execution to prevent world-nuking accidents (delete-all-documents, overwrite-critical-state).
- Context-aware — knows the shape of the user's Foundry world (actors, items, scenes, compendium).
- Intended use: AI-assisted macro generation for building out adventure content (actors, journals, items) without having to write JavaScript by hand.

**Introduction video (discovered 2026-04-21):** https://www.youtube.com/watch?v=6tp5h5Ja_ws — "2026 New - Free ScriptWright Safety-first Macro Vibe-coding for #FoundryVTT"

## Relevance to the DnD project

During content build (scene + NPC + journal creation for modules like Delian Tomb or Curse of Strahd), this is the right safety gate for the "Claude writes Foundry macros to batch-create content" workflow. Install when entering the heavy content-build phase.

**Paired with:** Claude.ai Project (which handles runtime NPC responses via REST API). ScriptWright is for build-time automation; Claude Project is for runtime interaction. Different surfaces, complementary.

**How to apply:**
- When the project enters the content-build phase (post-MVP), install ScriptWright and plan Claude-generated macros for actor/journal/item creation.
- Before running any AI-generated macro against the world, always use ScriptWright rather than pasting raw macros into Foundry's macro editor.
- Consider combining with the Foundry REST API we've already validated for cases where ScriptWright's scope doesn't cover (external triggers).
