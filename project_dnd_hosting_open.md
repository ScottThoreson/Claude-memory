---
name: DnD hosting decision (open)
description: Hosting is deferred; Pages viable for testing, server-side Claude proxy needed before production
type: project
originSessionId: a78ba36d-e093-4142-9f67-a84a32bcf57c
---
Hosting is not yet decided. Options on the table (2026-04-20):

| Option | Cost | Refactor needed | Works when Claude API is wired |
|---|---|---|---|
| Vercel | Free tier | None — native Next.js | Yes (API routes built in) |
| GitHub Pages + Firebase Cloud Functions | ~$0 (Blaze plan, credit card required) | Dynamic routes → query string | Yes |
| GitHub Pages + local Claude proxy on Scott's laptop | Free | Same as above | Yes, but laptop must be running at game time |

During the wizard-of-oz testing phase no server is required (human-Claude writes to RTDB directly), so any of the three work. The decision matters when we wire the real Claude API.

**Why:**
- User pushed back on the Vercel recommendation because they preferred keeping things on GitHub. That's legitimate — Pages + Functions is a real option, just fiddlier.
- User is also sensitive to cost ("so we're not paying for those API calls as we test stuff") — this biases toward Pages + no-server during testing.

**How to apply:**
- Don't commit the user to a host without explicit confirmation. The last standing question in the thread was the hosting pick.
- When resuming, surface the table above, note that the wizard-of-oz approach de-risks the decision, and push for a concrete pick so we can deploy the skeleton.
- If the answer is "Pages," plan for a routing refactor (dynamic path segments → query strings) before the first deploy. If "Vercel," zero refactor needed.
