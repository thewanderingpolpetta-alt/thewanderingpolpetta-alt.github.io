# my learnings

The owner's **personal homepage**: an interactive, minimal guide to the workflow they learned — going from an idea to a live website with **Claude Code, GitHub and GitHub Pages** — plus their next step (**Vercel**).

- **Live site:** https://thewanderingpolpetta-alt.github.io/
- **Repository:** https://github.com/thewanderingpolpetta-alt/thewanderingpolpetta-alt.github.io (public; a repo named `<username>.github.io` is automatically the user's GitHub Pages homepage, served from `main` /)
- **Owner:** GitHub account `thewanderingpolpetta-alt`
- **Sister project:** China Field Guide → https://github.com/thewanderingpolpetta-alt/china-field-guide (live at `/china-field-guide/` on the same domain). Its README documents the original project these learnings came from.

> This README is the full handoff. A new Claude (or person) should be able to continue from here without any earlier chat history.

---

## 1. How the owner likes to work

- **Not a developer.** Plain language, no jargon, no terminal work for them. If something interactive is needed (e.g. GitHub sign-in), run it in the background and give them just the code/link.
- **Design taste for this page:** minimalist **black and white**, clearly separated elements, flowing and easy to scan, **little text**. Technical details ("stored in localStorage" etc.) must **not** be front and center — hide them behind an **ⓘ / "Behind the scenes"** button or a tooltip.
- Content must stay **generic** (the workflow), not about China.
- **Preview and verify** before reporting success (desktop + phone width, no console errors, no horizontal scroll).
- **Never publish without being asked.** Publish = commit + push.

## 2. What's on the page

| Section | What it does |
|---|---|
| Hero | "Idea to live website" + one-line subtitle |
| Steps (`#steps`) | Interactive 8-step walkthrough: numbered dots with progress line, one card at a time, Back/Next + ← → keys. Each step: title, one-line lead, 3 short actions, optional **Show commands** drop-down (copy buttons), **ⓘ Behind the scenes** panel |
| Next (`#next`) | "Real apps with Vercel": Today (GitHub Pages) vs Next (Vercel) toggle over 6 rows, ⓘ panel with accurate caveats, planned steps 09–13 |
| Prompts (`#prompts`) | 9 cards — click copies the full reusable prompt (toast "Copied") |
| Fixes (`#fixes`) | Accordion: problem → one-line fix |
| Next ideas (`#ideas`) | Tiles that open on tap |
| Checklist (`#checklist`) | 9 items with progress counter; ⓘ tooltip explains ticks stay in this browser |
| Theme | ◐ button toggles light/dark (both strictly black & white) |

The 8 steps: **Start · Build · Preview · Media · Refine · GitHub · Publish · Update**.

## 3. How it's built

A **single `index.html`** (inline CSS + JS), no build step, no dependencies except Google Fonts (**Inter**, **JetBrains Mono**).

All content is in JavaScript arrays near the top of the `<script>` — edit those, not the HTML:

| Array | Content |
|---|---|
| `STEPS` | `{ short, title, lead, actions[3], code?[{cap, text, noCopy?}], behind[] }` |
| `COMPARE` | `[label, [pagesText, yes?], [vercelText, yes?]]` |
| `ROADMAP` | `[title, description]` — numbered after the last step (09…) |
| `PROMPTS` | `{ k, text }` |
| `FIXES` | `[problem, fixHTML]` |
| `IDEAS` | `[title, description]` |
| `CHECKS` | checklist strings |

Browser storage keys (per-viewer conveniences only): `learnings-step`, `learnings-checklist`, `learnings-theme`.

Accessibility: semantic sections, `aria-expanded`/`aria-current`, visible focus rings, keyboard navigation, `prefers-reduced-motion` respected.

## 4. Preview locally

```powershell
powershell -ExecutionPolicy Bypass -File serve.ps1            # http://localhost:8080
powershell -ExecutionPolicy Bypass -File serve.ps1 -port 8081  # another port
```

For Claude Code's browser preview, add a `.claude/launch.json` entry running `serve.ps1` (e.g. on 8081). Double-clicking `index.html` also works.

## 5. Publish

Environment: **Windows 11, Windows PowerShell 5.1**; Git at `C:\Program Files\Git\cmd`, GitHub CLI at `C:\Program Files\GitHub CLI` (installed via winget). If not on PATH: `$env:Path = "C:\Program Files\Git\cmd;C:\Program Files\GitHub CLI;" + $env:Path`.

```powershell
git add -A
git commit -m "Describe the change"
git push
gh api repos/thewanderingpolpetta-alt/thewanderingpolpetta-alt.github.io/pages/builds/latest --jq .status   # "built" = live
```

- Commit identity (repo-local): `thewanderingpolpetta-alt` / `348097017+thewanderingpolpetta-alt@users.noreply.github.com`.
- If GitHub isn't signed in on the machine: run `gh auth login --hostname github.com --git-protocol https --web` in the background, give the owner the one-time code + https://github.com/login/device, then `gh auth setup-git`.

## 6. Future direction: Vercel

The owner's plan for future interactive apps (already summarised on the page):
- **Private GitHub repository** (keeps history and logs, code not public) **deployed on Vercel** (free Hobby plan — personal, non-commercial use only).
- **Google sign-in** via a library such as **Auth.js** or **Clerk**, with a Google OAuth client.
- **Free database** from the Vercel Marketplace (e.g. **Neon Postgres**, **Supabase**).
- Secrets in **Vercel environment variables**, never in code.
- **Access control:** only chosen accounts can sign in. Vercel's built-in site-wide password protection is a **paid add-on**, so on the free plan restrict access through sign-in.
- Every push deploys automatically, with preview links per branch.

When that happens, add it to this page as real steps (move ROADMAP items into STEPS) and record new learnings, problems and prompts.

## 7. Ideas not done yet

Link the China guide from the homepage · CLAUDE.md template for new projects · starter template repo · custom domain · accessibility pass · fact-checking workflow for AI-written content.
