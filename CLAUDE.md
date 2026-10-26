# CLAUDE.md — my learnings (personal homepage)

Read **README.md** first: it is the complete handoff (page sections, content arrays, design rules, publishing, Vercel plan).

Working rules:
- The owner is not a developer: plain language, no terminal work for them; run interactive steps in the background and hand over just the code/link.
- Design: minimalist black & white, separated elements, **little text**. Technical details go behind ⓘ / "Behind the scenes" buttons, never front and center.
- Keep the content generic (the workflow), not project-specific.
- Single `index.html`; edit the content arrays (`STEPS`, `COMPARE`, `ROADMAP`, `PROMPTS`, `FIXES`, `IDEAS`, `CHECKS`), not hand-written HTML.
- Preview with `serve.ps1` and verify (desktop + phone width, console, no horizontal scroll) before reporting success.
- **Never publish without the owner saying so.** Publish = `git add -A; git commit; git push` (GitHub Pages, repo `thewanderingpolpetta-alt.github.io`).
- Git/gh: `C:\Program Files\Git\cmd`, `C:\Program Files\GitHub CLI` (Windows PowerShell 5.1).
- Future apps: private GitHub repo + Vercel (Google sign-in, free database, access via sign-in allowlist). See README §6.
