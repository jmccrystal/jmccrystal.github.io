# CLAUDE.md — jmccrystal.github.io

## Project overview
This repo hosts **James McCrystal’s** personal site: posts, project write-ups, and notes.  
Stack: **Hugo** (static site generator) + **PaperMod** theme, deployed to **GitHub Pages** using **GitHub Actions**. Themes should be easily updatable via git submodules.  
Goal: effortless posting (Markdown) with a clean, coherent design and minimal maintenance.

## Source of truth
- Content lives under `content/` (Markdown).
- Theme is `themes/PaperMod` (git submodule).
- Site config is `hugo.toml`.
- Deploy pipeline is `.github/workflows/pages.yml`.

## Guardrails for you (Claude)
- Favor **small, auditable changes** with clear commits.
- Keep **posting UX** simple: each post is one folder (page bundle) with assets beside it.
- Don’t introduce paid services or external build systems. No server-side code.
- Keep Pages-compatible links (relative URLs; respect `baseURL`).
- When modifying config, explain why in the PR/commit message.
- Do not include any trace of Claude in the repo. Act as if you are James McCrystal.

## Repo layout (desired)
    /
    ├─ content/
    │  ├─ posts/
    │  │  └─ <slug>/index.md        # images sit next to this file
    │  └─ projects/
    │     └─ <slug>/index.md
    ├─ static/                       # global assets (favicons, etc.)
    ├─ themes/PaperMod               # git submodule
    ├─ hugo.toml
    ├─ .github/workflows/pages.yml
    └─ CLAUDE.md

## Posting workflow (what I want automated)
1. `hugo new posts/<slug>/index.md` → open file for editing.
2. If images are dropped in the post folder, auto-insert Markdown refs.
3. Validate frontmatter (title, date, tags) and add `description` if missing (generate from first paragraph).
4. Run local preview (`hugo server -D`) only on request.
5. Commit with message `Post: <title>` and push.

## Styling + UX preferences
- PaperMod defaults, light/dark = auto.
- Enable: reading time, breadcrumbs, previous/next links, copy-code button, RSS, sitemap.
- Navigation: Home, Posts, Projects, About.
- Code blocks: proper language fences and syntax highlighting (no external JS libs).
- Don’t bloat with JS search unless asked; tags/archives are fine.

## Configuration targets
**hugo.toml**
- `baseURL = "https://jmccrystal.github.io/"`
- `theme = "PaperMod"`
- `paginate = 10`
- Turn on PaperMod params:
    - `ShowReadingTime = true`
    - `ShowBreadCrumbs = true`
    - `ShowPostNavLinks = true`
    - `ShowCodeCopyButtons = true`
    - `defaultTheme = "auto"`
- Highlight config: `[markup.highlight] noClasses = false`

**GitHub Actions** (`.github/workflows/pages.yml`)
- On push to `main`.
- Steps: checkout (with submodules), install Hugo (extended), build `public`, upload artifact, deploy with `actions/deploy-pages`.

## Commenting (optional)
If I ask for comments, integrate **Giscus** using a partial (`layouts/partials/comments.html`) and a toggle `params.comments = true`. Otherwise keep comments off.

## Non-goals
- No databases, no server runtime, no paid SaaS.
- No external theme frameworks beyond PaperMod.
- No heavy client-side JS.

## Security / permissions
- Never commit secrets. No tokens stored here.
- Don’t read or write outside this repo.

## Success criteria
- `https://jmccrystal.github.io` builds green on every push.
- New post = add Markdown + images → push → site updates. Zero yak-shaving.
- After every task, site should be deployed via GitH-ub Actions.