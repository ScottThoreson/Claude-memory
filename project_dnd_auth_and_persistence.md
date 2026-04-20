---
name: DnD auth + character persistence design
description: Firebase Auth per-user login; players keyed by auth.uid; characters live under /characters/{uid} and persist across sessions
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
Design direction (agreed 2026-04-20, not yet implemented):

- Every player authenticates individually via Firebase Auth. Specific method (email link / Google OAuth / email+password) deferred — Scott was going to check with the family's "Dad" about what everyone uses.
- RTDB schema switches from keying players by display name (Dad/Mom/Kid1/Kid2) to keying by stable Firebase `auth.uid`. Display name becomes a field on the player record, not the key.
- Character data is NOT per-session. It lives globally under `/characters/{uid}` and is referenced by sessions (e.g. `/sessions/{sid}/players/{uid}.characterId`). This lets a player keep the same fighter across the full 10–15-session campaign arc.
- Auth also gates the future Claude API route: unauthenticated requests bounce, and rate-limit/attribution is per-UID so a misbehaving user can be revoked individually.

**Why:**
- Per-user login enables persistent characters across sessions — the central campaign-scale goal in PROJECT_KNOWLEDGE.MD ("Same world across all campaigns. Characters and items persist").
- UID-keyed schema avoids a painful retrofit later. Retrofitting UID-keying onto a name-keyed schema means rewriting session code.
- Auth + server-side key is the only correct way to protect the Anthropic API key once it's wired. Auth is a layer on top, not a substitute.

**How to apply:**
- Recommendation is to fold auth in NOW, while the skeleton is still small, rather than after the wizard-of-oz loop works. Either order is viable but later costs more. User has not yet formally approved doing it now.
- When kids don't have their own email addresses, plan for Scott to pre-authorize the kid's device once (or a short-code-entry flow). Don't lock into a design that assumes every player reads their own email.
- Security rules move to `auth.uid != null` (plus an allowlist if we want only-family access) as soon as auth is live. Character paths should enforce `auth.uid == $uid` for writes.
