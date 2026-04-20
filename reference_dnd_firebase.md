---
name: DnD Firebase project coordinates
description: Firebase project ID, RTDB URL, GitHub repo, and local checkout paths for the DnD digital table
type: reference
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
- **Firebase project ID:** `dnd-thoresonws` (display name "DnD Game")
- **Firebase owner account:** `thoresonws@gmail.com`
- **RTDB URL:** `https://dnd-thoresonws-default-rtdb.firebaseio.com` (us-central1)
- **Firebase console:** https://console.firebase.google.com/project/dnd-thoresonws/overview
- **Web app ID:** `1:88596586523:web:665dc2256e6d008605d8be`
- **GitHub repo (canonical code):** https://github.com/thoresonws-pixel/DnD — canonical branch is `master` (not `main`); `main` is empty
- **PROJECT_KNOWLEDGE.MD:** https://github.com/thoresonws-pixel/DnD/blob/master/PROJECT_KNOWLEDGE.MD
- **Local checkout on work machine (sthoreson@imegcorp):** `c:\Users\sthoreson\source\repos\DnD-next`
- **Legacy Blazor prototype:** `c:\Users\sthoreson\source\repos\DnD` — abandoned, not the production target

During wizard-of-oz testing phase, Claude Code can read/write RTDB directly via REST:
- Read: `curl -s 'https://dnd-thoresonws-default-rtdb.firebaseio.com/<path>.json'`
- Patch: `curl -X PATCH -d '{...}' 'https://dnd-thoresonws-default-rtdb.firebaseio.com/<path>.json'`
Open rules (test mode) are active until ~2026-05-20; after that, rules must be tightened and service-account auth introduced for RTDB writes from here.
