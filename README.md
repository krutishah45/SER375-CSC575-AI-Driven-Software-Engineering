# SER375/CSC575 — AI Tools Course Companion

Static documentation site covering prompt engineering, AI agents, custom GPTs, and Claude Code, built for GitHub Pages using the [Just the Docs](https://just-the-docs.com/) Jekyll theme (loaded remotely — no local build required to publish).

## Repository layout

```
.
├── _config.yml                      # Jekyll + Just the Docs configuration
├── index.md                         # Home page (nav_order: 1)
├── 01-prompt-engineering.md         # Guide 1
├── 02-ai-agents-agentic-workflows.md# Guide 2
├── 03-custom-gpts-ai-assistants.md  # Guide 3
├── 04-claude-code-basics.md         # Guide 4
├── 05-choosing-the-right-tool.md    # Guide 5
├── 06-faq-troubleshooting.md        # FAQ / troubleshooting
├── 07-worked-case-study.md          # End-to-end worked example
├── glossary.md                      # Term definitions
├── references.md                    # Consolidated external links
└── assets/                          # Original SVG diagrams (no third-party images)
```

**Important:** `_config.yml` must sit at the repository root, at the same level as `index.md` — not nested in a subfolder. If you unzip this into an existing repo that already has content, move these files to the root (or into a `docs/` folder and point GitHub Pages at `/docs`, adjusting paths if so).

## Publish it on GitHub Pages (no local install needed)

1. Push this content to a GitHub repository (public, or private on a plan that supports Pages).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, select **Deploy from a branch**.
4. Choose the branch (usually `main`) and the root folder (`/`), then **Save**.
5. Wait a few minutes — GitHub will build the Jekyll site automatically (Just the Docs loads via `remote_theme`, which GitHub Pages supports natively; no Gemfile or local `bundle install` needed).
6. Your site will be live at `https://<your-username>.github.io/<repo-name>/`.

### One config value to double-check after your first publish

Open `_config.yml` and confirm `baseurl` matches your actual URL path:
- If your site is at `https://<username>.github.io/<repo-name>/`, set `baseurl: "/<repo-name>"`.
- If it's a user/org root site (`https://<username>.github.io/`), leave `baseurl: ""`.

Get the exact URL from **Settings → Pages** after the first successful build, then update and re-push if needed.

## Previewing changes locally (optional)

You don't need this to publish — GitHub builds it for you. It's only useful if you want to preview edits before pushing.

```bash
gem install bundler jekyll
bundle init
echo 'gem "just-the-docs"' >> Gemfile
echo 'gem "jekyll-remote-theme"' >> Gemfile
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

## Editing content

Every guide page is plain Markdown with a small YAML front-matter block controlling its title and sidebar position:

```yaml
---
title: "Guide 1: Prompt Engineering"
nav_order: 2
---
```

To add a new page, create a `.md` file with front matter following the same pattern (pick an unused `nav_order` number), and it will automatically appear in the sidebar — no other configuration needed.

## Maintenance note

Pricing, product names, and tool availability (Guide 5, references.md) change frequently. Everything sourced from a vendor's pricing/help page is dated and linked — re-verify before reusing this content in a future semester.
